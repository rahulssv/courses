# Service
```java title="BatchService.java"
package com.jt.service;
import java.util.Date;
import java.util.List;
import java.util.Optional;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.scheduling.annotation.Scheduled;
import org.springframework.stereotype.Service;

import com.jt.model.batch.Status;
import com.jt.model.batch.Booking;
import com.jt.model.batch.TourBatch;
import com.jt.model.tour.GuidedTour;
import com.jt.model.user.Traveller;
import com.jt.repository.TourRepository;
import com.jt.repository.BatchRepository;
import com.jt.repository.BookingRepository;

@Service
public class BatchService {

	@Autowired
	private BatchRepository tourBatchRepository;
	private TourBatch batch;
	@Autowired
	private TourRepository guidedTourRepository;
	private GuidedTour tour;

	@Autowired
	private BookingRepository bookingRepository;
	private List<Booking> bookings;

	public Booking bookTraveller(Booking booking) {

		try {
			
			Optional<TourBatch> fetchedBatch = this.tourBatchRepository.findById(booking.getBatchId());
			if(fetchedBatch.isPresent()) {
				this.batch = fetchedBatch.get();
				if (this.batch.getAvailableSeats() - booking.getTravellers().size() >= 0) {
					this.bookingRepository.save(booking);
					bookings = this.bookingRepository.findAllByBatchId(booking.getBatchId());
					int bookedSeats = 0;
					int sequence = this.batch.getCapacity() - this.batch.getAvailableSeats();
					for (Booking booked : bookings) {
						bookedSeats += booked.getTravellers().size();
					}
					List<Traveller> travellers = booking.getTravellers();
					for (Traveller traveller : travellers) {
						traveller.setBookingSequence(++sequence);
					}
					this.batch.setAvailableSeats(bookedSeats);
					this.tourBatchRepository.save(this.batch);
					return booking;
			}
			return null;
			} else {
				return null;
			}
		} catch (Exception e) {
			return null;
		}

	}

	public TourBatch addBatch(Long tour_id, TourBatch batch) {
		try {
			Optional<GuidedTour> fetchedTour = this.guidedTourRepository.findById(tour_id);
			if(fetchedTour.isPresent()) {				
				this.tour = fetchedTour.get();
				batch.setTour(this.tour);
				batch.setEndDate(this.tour.getDays());
				batch.setStatus("Active");
				batch.getGuide().setBookingSequence(0);
				int bookedSeats = 0;
				batch.setAvailableSeats(bookedSeats);
				this.tourBatchRepository.save(batch);
				return batch;
			}
			return null;
		} catch (Exception e) {
			System.out.println(e.getMessage());
			return null;
		}
		
	}

	public List<TourBatch> getBatchesByUser() {
		return tourBatchRepository.findAllByStatus(Status.ACTIVE);
	}

	public List<TourBatch> getBatchesByTourId(Long tourId) {
		GuidedTour tour = guidedTourRepository.findById(tourId).orElse(null);
		if (tour != null)
			return tourBatchRepository.findAllByTourId(tourId);
		return null;

	}

	public List<TourBatch> getBatchesByTourIdByUser(Long tourId) {
		GuidedTour tour = guidedTourRepository.findById(tourId).orElse(null);
		if (tour != null) {
			return tourBatchRepository.findAllByTourIdAndStatus(tourId, Status.ACTIVE);
		}
		return null;

	}

	public List<TourBatch> getBatches() {
		try {
			return (List<TourBatch>) this.tourBatchRepository.findAll();
		} catch (Exception e) {
			return null;
		}
	}

	public TourBatch getBatchById(Long batch_id) {
		try {
			Optional<TourBatch> fetchedBatch = this.tourBatchRepository.findById(batch_id);
			if(fetchedBatch.isPresent()) {
				return fetchedBatch.get();
			}
			return null;
		} catch (Exception e) {
			return null;
		}

	}

	public boolean deleteBatchById(Long batch_id) {
		try {
			Optional<TourBatch> fetchedBatch = this.tourBatchRepository.findById(batch_id);
			if (fetchedBatch.isPresent()) {
				this.batch = fetchedBatch.get();
				this.batch.setStatus("Cancelled");
				this.tourBatchRepository.save(this.batch);
				return true;
			}
			else {
				return false;
			}		
		} catch (Exception e) {
			return false;
		}

	}

	public TourBatch updateBatch(TourBatch batch) {
		if (this.getBatchById(batch.getId()) != null) {
			return tourBatchRepository.save(batch);
		}
		return null;
	}

	public List<TourBatch> getFilteredBatches(Date minDate, Date maxDate) {

		if (maxDate == null && minDate == null)
			return null;

		if (minDate != null) {
			if (maxDate != null) {
				if (minDate.after(maxDate))
					return null;
				return tourBatchRepository.findBatchesBetween(minDate, maxDate);
			}
			return tourBatchRepository.findBatchesAfter(minDate);
		}
		return tourBatchRepository.findBatchesBefore(maxDate);
	}

	@Scheduled(cron = "0 2 0 * * *")
	public void updateStatus() {
		System.out.println("Updating Status of TourBatch on date-change");
		tourBatchRepository.updateStatus();
	}

	public List<TourBatch> getFilteredStatus(Status status) {
		return tourBatchRepository.findBatchByStatus(status);
	}

	public List<TourBatch> getFilteredAvailableSeats(int minAvailableSeats, int maxAvailableSeats) {
		if (minAvailableSeats == -1 && maxAvailableSeats == -1) {
			return null;
		}
		if (minAvailableSeats == -1) {
			return tourBatchRepository.findMaxAvailableSeats(maxAvailableSeats);
		} else if (maxAvailableSeats == -1) {
			return tourBatchRepository.findMinAvailableSeats(minAvailableSeats);
		} else if (minAvailableSeats <= maxAvailableSeats) {
			return tourBatchRepository.findFilteredAvailableSeats(minAvailableSeats, maxAvailableSeats);
		}
		return null;
	}

	public List<TourBatch> getFilteredPrice(double budget) {
		if (budget < 0 || budget > 10000000)
			return null;
		return tourBatchRepository.findFilteredPrice(budget);
	}

}

```
```java title="BookingService.java"
package com.jt.service;

import java.util.List;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

import com.jt.model.batch.Booking;
import com.jt.repository.BookingRepository;

@Service
public class BookingService {

	@Autowired
	private BookingRepository bookingRepository;

	public List<Booking> getAllBookings() {

		try {
			return (List<Booking>) this.bookingRepository.findAll();
		} catch (Exception e) {
			return null;
		}

	}
	
	public List<Booking> getAllBookingsUser(String username){
		try {
			return (List<Booking>) this.bookingRepository.findAllByUsername(username) ;
		}catch(Exception e) {
			return null ;
		}
	}
}

```
```java title="JwtService.java"
package com.jt.service;

import java.security.Key;
import java.util.Date;
import java.util.HashMap;
import java.util.Map;
import java.util.function.Function;

import org.springframework.security.core.userdetails.UserDetails;
import org.springframework.stereotype.Component;

import io.jsonwebtoken.Claims;
import io.jsonwebtoken.Jwts;
import io.jsonwebtoken.SignatureAlgorithm;
import io.jsonwebtoken.io.Decoders;
import io.jsonwebtoken.security.Keys;

@Component
public class JwtService {
	public static final String SECRET = "5367566B59703373367639792F423F4528482B4D6251655468576D5A71347437";

	
	public String extractUsername(String token) {
        return extractClaim(token, Claims::getSubject);
    }

    public Date extractExpiration(String token) {
        return extractClaim(token, Claims::getExpiration);
    }

    public <T> T extractClaim(String token, Function<Claims, T> claimsResolver) {
        final Claims claims = extractAllClaims(token);
        return claimsResolver.apply(claims);
    }

    private Claims extractAllClaims(String token) {
        return Jwts
                .parserBuilder()
                .setSigningKey(getSignKey())
                .build()
                .parseClaimsJws(token)
                .getBody();
    }

    private Boolean isTokenExpired(String token) {
        return extractExpiration(token).before(new Date());
    }

    public Boolean validateToken(String token, UserDetails userDetails) {
        final String username = extractUsername(token);
        return (username.equals(userDetails.getUsername()) && !isTokenExpired(token));
    }

	
	public String generateToken(String userName) {
		Map<String,Object> claims = new HashMap<>() ;
		return createToken(claims,userName);
	}

	private String createToken(Map<String, Object> claims, String userName) {
		
		return Jwts.builder()
				.setClaims(claims)
				.setSubject(userName)
				.setIssuedAt(new Date(System.currentTimeMillis()))
				.setExpiration(new Date(System.currentTimeMillis()+1000*60*30))
				.signWith(getSignKey(),SignatureAlgorithm.HS256).compact();
				
	}

	private Key getSignKey() {
		byte[] keyBytes = Decoders.BASE64.decode(SECRET);
		return Keys.hmacShaKeyFor(keyBytes);
	}
}

```
```java title="MetadataService.java"
package com.jt.service;

import java.util.List;

import org.springframework.stereotype.Service;

import com.jt.model.DisplayPair;
import com.jt.model.batch.Status;
import com.jt.model.tour.DifficultyLevel;
import com.jt.model.tour.Mode;
import com.jt.model.tour.RoomType;
import com.jt.model.auth.Role;

@Service
public class MetadataService {

	public List<DisplayPair<String, String>> allDifficultyLevels() {
		try {
			return DifficultyLevel.getDisplayPairs();
		} catch (Exception e) {
			return null;
		}
		
	}

	public List<DisplayPair<String, String>> allModes() {
		try {
			return Mode.getDisplayPairs();
		} catch (Exception e) {
			return null;
		}
		
	}

	public List<DisplayPair<String, String>> allRoomTypes() {
		try {
			return RoomType.getDisplayPairs();
		} catch (Exception e) {
			return null;
		}
		
	}

	public List<DisplayPair<String, String>> allRoles() {
		try {
			return Role.getDisplayPairs();
		} catch (Exception e) {
			return null;
		}
		
	}

	public List<DisplayPair<String, String>> allStatus() {
		try {
			return Status.getDisplayPairs();
		} catch (Exception e) {
			return null;
		}
		
	}

}

```
```java title="TourService.java"
package com.jt.service;

import java.util.Collections;
import java.util.List;
import java.util.Optional;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

import com.jt.model.batch.TourBatch;
import com.jt.model.tour.DifficultyLevel;
import com.jt.model.tour.GuidedTour;
import com.jt.model.tour.Mode;
import com.jt.repository.TourRepository;
import com.jt.repository.BatchRepository;

@Service
public class TourService {
	@Autowired
	private TourRepository guidedTourRepository;
	GuidedTour tour;
	@Autowired
	private BatchRepository tourBatchRepository;
	
	public List<GuidedTour> filterTourByDuration(int minDays, int maxDays) {
		if ((minDays == -1 && maxDays == Integer.MAX_VALUE) || (minDays > maxDays))
			return Collections.emptyList();
		return guidedTourRepository.filterTourByDuration(minDays, maxDays);
	}

	public GuidedTour addTour(GuidedTour tour) {
		try {
			tour.setDays(tour.getItinerary().getDayPlans().size());
			guidedTourRepository.save(tour);

		} catch (Exception e) {
			return null;
		}
		return tour;
	}

	public List<GuidedTour> getTours() {
		try {
			return (List<GuidedTour>) guidedTourRepository.findAll();
		} catch (Exception e) {
			return null;
		}
	}
	
	public GuidedTour getTourById(Long id) {
		try {
			Optional<GuidedTour> fetchedTour = this.guidedTourRepository.findById(id);
			if(fetchedTour.isPresent()) {
				return fetchedTour.get();
			}
			return null;
		} catch (Exception e) {
			return null;
		}
	}

	public Boolean deleteTourById(Long id) {
		try {
			this.guidedTourRepository.deleteById(id);
			return true;
		} catch (Exception e) {
			return false;
		}
	}

	public GuidedTour updateTour(GuidedTour updateTour) {

		try {
			this.guidedTourRepository.save(updateTour);
			return getTourById(updateTour.getId());
		} catch (Exception e) {
			return null;
		}

	}

	public List<TourBatch> getTourBatches(Long tourId) {

		try {
			return this.tourBatchRepository.findAllByTourId(tourId);

		} catch (Exception e) {
			return null;
		}

	}
	
	public List<GuidedTour> filteredToursByPlace(String source, String destination) {
		 
		if (source == null && destination == null)
			return (List<GuidedTour>) guidedTourRepository.findAll();
		if (source != null) {
			if (destination != null) {
				if (source.equals(destination))
					return null;
				return guidedTourRepository.filterToursByPlaceBetween(source, destination);
			}
			return guidedTourRepository.filterToursByPlaceSource(source);
		}
		return guidedTourRepository.filterToursByPlaceDestination(destination);
	}
	
	public List<GuidedTour> filteredToursByMode(Mode mode) {
 
		if (mode == null)
			return (List<GuidedTour>) guidedTourRepository.findAll();
 
		return guidedTourRepository.filterToursByMode(mode);
	}
	
	public List<GuidedTour> filteredToursByDifficultyLevel(DifficultyLevel difficultyLevel) {
 
		if (difficultyLevel == null)
			return (List<GuidedTour>) guidedTourRepository.findAll();
 
		return guidedTourRepository.filteredToursByDifficultyLevel(difficultyLevel);
	}

	public List<GuidedTour> getMostPopularTours() {
		try {
			return guidedTourRepository.findMostPopularTours();
		}
		catch(Exception e) {
			return null;
		}
	}
}

```
```java title="UserService.java"
package com.jt.service;

import java.util.List;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.security.crypto.password.PasswordEncoder;
import org.springframework.stereotype.Service;

import com.jt.model.auth.Role;
import com.jt.model.auth.User;
import com.jt.repository.UserRepository;

@Service
public class UserService {
	@Autowired
	private UserRepository userRepo ;
	
	@Autowired
	private PasswordEncoder passwordEncoder ;

	public User createTheUser(User user) {
		String role = user.getRole().toString() ;

			if(role.equals("ADMIN")) {
				User u = userRepo.findByRole(Role.valueOf("ADMIN")) ;
				if(u==null) {
					user.setPassword(passwordEncoder.encode(user.getPassword()));
					return userRepo.save(user) ;
				}
				else {
					return null ;
				}
			}
			else {
				User u = userRepo.findByUserName(user.getUserName()).orElse(null) ;
				System.out.println("user"+u) ;
				if(u==null) {
					user.setPassword(passwordEncoder.encode(user.getPassword()));
					return userRepo.save(user) ;
				}
				return null ;
			}
		
		
	}
	
	public  List<User> getAllTheUsers() {
		try {
			return (List<User>) this.userRepo.findAll();
		}catch(Exception e) {
			return null;
		}
	}
	
}

```
