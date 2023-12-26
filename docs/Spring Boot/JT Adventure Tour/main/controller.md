## Controller.java
```java title="AuthController.java"
package com.jt.controller;
import java.util.Optional;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.security.authentication.AuthenticationManager;
import org.springframework.security.authentication.UsernamePasswordAuthenticationToken;
import org.springframework.security.core.Authentication;
import org.springframework.security.core.userdetails.UsernameNotFoundException;
import org.springframework.web.bind.annotation.CrossOrigin;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

import com.jt.auth.AuthRequest;
import com.jt.auth.AuthResponse;
import com.jt.model.auth.User;
import com.jt.repository.UserRepository;
import com.jt.service.JwtService;
import com.jt.service.UserService;

@RestController
@CrossOrigin(origins = "*")
@RequestMapping("/auth")
public class AuthController {
	@Autowired
	private UserService service ;
	
	@Autowired
	private JwtService jwtService ;
	
	@Autowired
	private UserRepository userRepo ;
	
	@Autowired
	private AuthenticationManager authenticationManager ;
	
		
	@PostMapping("/login")
	public AuthResponse authenticateAndGetToken(@RequestBody AuthRequest authRequest) {
		Authentication authentication = authenticationManager.authenticate(new UsernamePasswordAuthenticationToken(authRequest.getUserName(), authRequest.getPassword()));
		if(authentication.isAuthenticated()) {
			Optional<User> fetchedUser = userRepo.findByUserName(authRequest.getUserName());
			if(fetchedUser.isPresent()) {
				String role = fetchedUser.get().getRole().toString() ;
				String token = jwtService.generateToken(authRequest.getUserName()) ;
				AuthResponse authResponse = new AuthResponse() ;
				authResponse.setToken(token) ;
				authResponse.setRole(role) ;
				authResponse.setUsername(authRequest.getUserName()) ;
				return authResponse ;
			}
			throw new UsernameNotFoundException("invalid user request !") ;
		}
		else {
			throw new UsernameNotFoundException("invalid user request !") ;
		}
		
	}
	
	@PostMapping("/register")
	public ResponseEntity<HttpStatus> createUser(@RequestBody User user) {
			User u = service.createTheUser(user) ;
			if(u!=null)
				return new ResponseEntity<HttpStatus>(HttpStatus.CREATED) ;
			else
				return new ResponseEntity<HttpStatus>(HttpStatus.NOT_ACCEPTABLE) ; 
	}

}

```
```java title="BatchController.java"
package com.jt.controller;


import java.util.Date;
import java.util.List;


import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.format.annotation.DateTimeFormat;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.security.access.prepost.PreAuthorize;
import org.springframework.security.core.annotation.AuthenticationPrincipal;
import org.springframework.web.bind.annotation.CrossOrigin;
import org.springframework.web.bind.annotation.DeleteMapping;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.PutMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;

import com.jt.config.UserInfoUserDetails;
import com.jt.model.batch.Booking;
import com.jt.model.batch.Status;
import com.jt.model.batch.TourBatch;
import com.jt.service.BatchService;

@RequestMapping("/batches")
@RestController
@CrossOrigin(origins = "*")
public class BatchController {

	@Autowired
	private BatchService batchService;
	
	@PostMapping("/book")
	@PreAuthorize("hasAuthority('CUSTOMER')")
	public ResponseEntity<Booking> bookTraveller(@RequestBody Booking booking) {
		Booking newbooking = batchService.bookTraveller(booking);
		if (newbooking != null) {
			return new ResponseEntity<Booking>(newbooking, HttpStatus.CREATED);
		}
		return new ResponseEntity<Booking>(newbooking, HttpStatus.NOT_ACCEPTABLE);
	}

	
	@PostMapping("/tours/{tourId}")
	@PreAuthorize("hasAuthority('ADMIN')")
	public ResponseEntity<TourBatch> createBatch(@PathVariable Long tourId, @RequestBody TourBatch batch) {
		if(this.batchService.addBatch(tourId, batch)!=null) {
			return new ResponseEntity<TourBatch>(batch,HttpStatus.CREATED);
		}
		return new ResponseEntity<TourBatch>(HttpStatus.NOT_FOUND);
	}

	
	@GetMapping()
	public ResponseEntity< List<TourBatch>> getAllBatches(@AuthenticationPrincipal UserInfoUserDetails userDetails){
		// checking whether someone is logged in or not based on that showing the batches
		System.out.println("inside get batches");
		if(userDetails!=null && userDetails.getAuthorities().stream()
				.anyMatch(a->a.getAuthority().equals("ADMIN"))) {
			List<TourBatch> batches = batchService.getBatches();
			if(batches != null)
				return new ResponseEntity<List<TourBatch>>(batches,HttpStatus.OK);
			return new ResponseEntity<List<TourBatch>>(HttpStatus.NOT_FOUND);
		}else {
			List<TourBatch> batches = batchService.getBatchesByUser();
			if(batches != null)
				return new ResponseEntity<List<TourBatch>>(batches,HttpStatus.OK);
			return new ResponseEntity<List<TourBatch>>(HttpStatus.NOT_FOUND);
		}
		
	}
	
	
	@PutMapping()
	@PreAuthorize("hasAuthority('ADMIN')")
	public ResponseEntity<TourBatch> updateBatch(@RequestBody TourBatch tourBatch) {
		TourBatch updatedBatch = batchService.updateBatch(tourBatch);
		if(updatedBatch!=null) {
			return new ResponseEntity<TourBatch>(updatedBatch,HttpStatus.OK);
		}
		return new ResponseEntity<TourBatch>(tourBatch,HttpStatus.NOT_MODIFIED);
	}
	
	
	@GetMapping("/{batchId}")
	public ResponseEntity<TourBatch> getBatchById(@PathVariable Long batchId) {
		TourBatch batch =  batchService.getBatchById(batchId);
		if(batch!=null) 
			 return new ResponseEntity<TourBatch>(batch,HttpStatus.FOUND);
		return new ResponseEntity<TourBatch>(HttpStatus.NOT_FOUND);
	}
	
	@DeleteMapping("/{batchId}")
	@PreAuthorize("hasAuthority('ADMIN')")
	public ResponseEntity<HttpStatus> deleteBatchById(@PathVariable Long batchId) {
		if( batchService.deleteBatchById(batchId) == true) {
			return new ResponseEntity<HttpStatus>(HttpStatus.OK);
		}
		return new ResponseEntity<HttpStatus>(HttpStatus.NOT_ACCEPTABLE); 
	}
	
	@GetMapping("/startDate")
	public ResponseEntity< List<TourBatch>> getFilteredBatches(
			@RequestParam(value = "minDate", required = false) @DateTimeFormat(pattern = "yyyy-MM-dd") Date minDate,
			@RequestParam(value = "maxDate", required = false) @DateTimeFormat(pattern = "yyyy-MM-dd") Date maxDate) {
		List<TourBatch> batches = batchService.getFilteredBatches(minDate, maxDate);
		return new ResponseEntity<List<TourBatch>>(batches,HttpStatus.OK);
	}
	
	@GetMapping("/status")
	public ResponseEntity<List<TourBatch>> getFilteredStatus(
			@RequestParam(value = "status") Status status) {
		List<TourBatch> tourBatch=batchService.getFilteredStatus(status);
		if(tourBatch!=null && !tourBatch.isEmpty()) {
			return new ResponseEntity<List<TourBatch>>(tourBatch,HttpStatus.OK);
		}
		return new ResponseEntity<List<TourBatch>>(HttpStatus.NOT_FOUND);
	}
	
	@GetMapping("/availableSeats")
	public ResponseEntity<List<TourBatch>> getFilteredAvailableSeats(
			@RequestParam(value = "minAvailableSeats", required = false, defaultValue="-1") int minAvailableSeats,
			@RequestParam(value = "maxAvailableSeats", required = false, defaultValue="-1") int maxAvailableSeats) {
		List<TourBatch> tourBatch=batchService.getFilteredAvailableSeats(minAvailableSeats, maxAvailableSeats);
		if(tourBatch!=null && !tourBatch.isEmpty() ) {
			return new ResponseEntity<List<TourBatch>>(tourBatch,HttpStatus.OK);
		}
		return new ResponseEntity<List<TourBatch>>(HttpStatus.NOT_FOUND);
	}
	
	@GetMapping("/perParticipantCost")
	public ResponseEntity<List<TourBatch>> getFilteredPrice(
			@RequestParam(value = "budget") double budget) {
		List<TourBatch> tourBatch=batchService.getFilteredPrice(budget);
		if(tourBatch!=null && !tourBatch.isEmpty()) {
			return new ResponseEntity<List<TourBatch>>(tourBatch,HttpStatus.OK);
		}
		return new ResponseEntity<List<TourBatch>>(HttpStatus.NOT_FOUND);
	}
}


```
```java title="BookingController.java"
package com.jt.controller;

import java.util.List;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.security.core.annotation.AuthenticationPrincipal;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

import com.jt.config.UserInfoUserDetails;
import com.jt.model.batch.Booking;
import com.jt.service.BookingService;

@RequestMapping("/bookings")
@RestController
public class BookingController {
	@Autowired
	private BookingService service;
	
	@GetMapping()
	public ResponseEntity<List<Booking>> getBookings(@AuthenticationPrincipal UserInfoUserDetails userDetails) {
		List<Booking> bookings = null ;
		Boolean isAdmin=userDetails.getAuthorities().stream().anyMatch(a->a.getAuthority().equals("ADMIN"));
		if(userDetails!=null && isAdmin)
				bookings = service.getAllBookings();			
		else
			bookings = service.getAllBookingsUser(userDetails.getUsername());
		
		if(bookings!=null) {
			return new ResponseEntity<List<Booking>>(bookings,HttpStatus.OK);
		}
		return new ResponseEntity<List<Booking>>(bookings, HttpStatus.NOT_FOUND);
		
	}
}


```
```java title="MetadataController.java"
package com.jt.controller;
import java.util.List;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.web.bind.annotation.CrossOrigin;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

import com.jt.model.DisplayPair;
import com.jt.service.MetadataService;

@RestController
@RequestMapping("/metadata")
@CrossOrigin(origins = "*")
public class MetadataController {
	@Autowired
	private MetadataService service;

	@GetMapping("/difficulties")
	public ResponseEntity<List<DisplayPair<String, String>>> getDifficultyLevels(){
		List<DisplayPair<String, String>>difficultyLevels =service.allDifficultyLevels();
		if(difficultyLevels!=null) {
			return new ResponseEntity<List<DisplayPair<String,String>>>(difficultyLevels,HttpStatus.OK);
		}
		return new ResponseEntity<List<DisplayPair<String,String>>>(HttpStatus.NOT_FOUND);
	}
	@GetMapping("/modes")
	public ResponseEntity<List<DisplayPair<String, String>>> getModes(){ 
		List<DisplayPair<String, String>>modes =service.allModes();
		if(modes!=null) {
			return new ResponseEntity<List<DisplayPair<String,String>>>(modes,HttpStatus.OK);
		}
		return new ResponseEntity<List<DisplayPair<String,String>>>(HttpStatus.NOT_FOUND);
	}
	@GetMapping("/roomtypes")
	public ResponseEntity<List<DisplayPair<String, String>>> getRoomTypes(){
		
		List<DisplayPair<String, String>>roomTypes =service.allRoomTypes();
		if(roomTypes!=null) {
			return new ResponseEntity<List<DisplayPair<String,String>>>(roomTypes,HttpStatus.OK);
		}
		return new ResponseEntity<List<DisplayPair<String,String>>>(HttpStatus.NOT_FOUND);
	}
	@GetMapping("/roles")
	public ResponseEntity<List<DisplayPair<String, String>>> getRoles(){
		List<DisplayPair<String, String>>roles =service.allRoles();
		if(roles!=null) {
			return new ResponseEntity<List<DisplayPair<String,String>>>(roles,HttpStatus.OK);
		}
		return new ResponseEntity<List<DisplayPair<String,String>>>(HttpStatus.NOT_FOUND);
	}
	@GetMapping("/batchstatuses")
	public ResponseEntity<List<DisplayPair<String, String>>> getStatus(){
		List<DisplayPair<String, String>>status =service.allStatus();
		if(status!=null) {
			return new ResponseEntity<List<DisplayPair<String,String>>>(status,HttpStatus.OK);
		}
		return new ResponseEntity<List<DisplayPair<String,String>>>(HttpStatus.NOT_FOUND);
	}

}


```
```java title="TourController.java"
package com.jt.controller;

import java.util.List;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.security.access.prepost.PreAuthorize;
import org.springframework.security.core.annotation.AuthenticationPrincipal;
import org.springframework.web.bind.annotation.CrossOrigin;
import org.springframework.web.bind.annotation.DeleteMapping;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PathVariable;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.PutMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RequestParam;
import org.springframework.web.bind.annotation.RestController;

import com.jt.config.UserInfoUserDetails;
import com.jt.model.batch.TourBatch;
import com.jt.model.tour.DifficultyLevel;
import com.jt.model.tour.GuidedTour;
import com.jt.model.tour.Mode;
import com.jt.service.BatchService;
import com.jt.service.TourService;

@RequestMapping("/tours")
@CrossOrigin(origins = "*")
@RestController
public class TourController {
	@Autowired
	private TourService tourService;
	@Autowired
	private BatchService batchService;
	
	@GetMapping("/day")
	public ResponseEntity<List<GuidedTour>> filterTourByDuration(
			@RequestParam(value = "minDays", required=false, defaultValue="-1" ) int minDays,
			@RequestParam(value = "maxDays", required=false, defaultValue=""+Integer.MAX_VALUE) int maxDays) {
		
		List<GuidedTour> guidedTour=tourService.filterTourByDuration(minDays,maxDays);
		if(!guidedTour.isEmpty()) {
			return new ResponseEntity<List<GuidedTour>>(guidedTour,HttpStatus.OK);
		}
		return new ResponseEntity<List<GuidedTour>>(HttpStatus.NOT_FOUND);
	}
	

	
	@GetMapping("/place")
	public ResponseEntity<List<GuidedTour>> filteredToursByPlace(
			@RequestParam(value = "source", required = false) String source,
			@RequestParam(value = "destination", required = false) String destination) {
		List<GuidedTour> tours = tourService.filteredToursByPlace(source, destination);
		if(!tours.isEmpty()) {
			return new ResponseEntity<List<GuidedTour>>(tours,HttpStatus.OK);
		}
		return new ResponseEntity<List<GuidedTour>>(HttpStatus.NOT_FOUND);
	}
	
	@GetMapping("/mode")
	public ResponseEntity<List<GuidedTour>> filteredToursByMode(
			@RequestParam(value = "mode", required = false) String mode) {
		List<GuidedTour> tours = tourService.filteredToursByMode(Mode.fromString(mode));
		if(!tours.isEmpty()) {
			return new ResponseEntity<List<GuidedTour>>(tours,HttpStatus.OK);
		}
		return new ResponseEntity<List<GuidedTour>>(HttpStatus.NOT_FOUND);
	}
	
	@GetMapping("/difficultyLevel")
	public ResponseEntity<List<GuidedTour>> filteredToursByDifficultyLevel(
			@RequestParam(value = "difficultyLevel", required = false) String difficultyLevel) {
		List<GuidedTour> tours = tourService.filteredToursByDifficultyLevel(DifficultyLevel.fromString(difficultyLevel));
		if(!tours.isEmpty()) {
			return new ResponseEntity<List<GuidedTour>>(tours,HttpStatus.OK);
		}
		return new ResponseEntity<List<GuidedTour>>(HttpStatus.NOT_FOUND);
	}
	
	
	@GetMapping("/popular")
	public ResponseEntity<List<GuidedTour>> getMostPopularTours() {
	    List<GuidedTour> tours = tourService.getMostPopularTours();
	    if (tours != null) {
	        return new ResponseEntity<>(tours, HttpStatus.OK);
	    }
	    return new ResponseEntity<>(HttpStatus.NOT_FOUND);
	}
	
	
	
	@PostMapping()
	@PreAuthorize("hasAuthority('ADMIN')")
	public ResponseEntity<GuidedTour> saveTour(@RequestBody GuidedTour tour) {
		
		System.out.println("inside tour save tour");
		if (tourService.addTour(tour) != null) {
			return new ResponseEntity<GuidedTour>(tour, HttpStatus.CREATED);
		}
		return new ResponseEntity<GuidedTour>(HttpStatus.NOT_ACCEPTABLE);
	}
	@GetMapping()
	public ResponseEntity<List<GuidedTour>> getTours() {
		List<GuidedTour> tours = tourService.getTours();
		if (tours != null)
			return new ResponseEntity<List<GuidedTour>>(tours, HttpStatus.OK);
		return new ResponseEntity<>(HttpStatus.NOT_FOUND);
	}

	@GetMapping("/{id}")
	public ResponseEntity<GuidedTour> getTourById(@PathVariable Long id) {
		GuidedTour tour = tourService.getTourById(id);
		if (tour != null)
			return new ResponseEntity<GuidedTour>(tour, HttpStatus.OK);
		return new ResponseEntity<>(HttpStatus.NOT_FOUND);
	}

	@GetMapping("/{tourId}/batches")
	public ResponseEntity<List<TourBatch>> getBatchesByTourId(@PathVariable Long tourId , @AuthenticationPrincipal UserInfoUserDetails userDetails) {
		
		if(userDetails!=null && userDetails.getAuthorities().stream()
				.anyMatch(a -> a.getAuthority().equals("ADMIN"))) {
			
			List<TourBatch> tourBatches = batchService.getBatchesByTourId(tourId);
			if (tourBatches != null)
				return new ResponseEntity<List<TourBatch>>(tourBatches, HttpStatus.OK);
			return new ResponseEntity<List<TourBatch>>(HttpStatus.NOT_FOUND);
		}
		else {
			List<TourBatch> tourBatches = batchService.getBatchesByTourIdByUser(tourId);
			if (tourBatches != null)
				return new ResponseEntity<List<TourBatch>>(tourBatches, HttpStatus.OK);
			return new ResponseEntity<List<TourBatch>>(HttpStatus.NOT_FOUND);
		}
	}
	
	
	
	@PutMapping()
	@PreAuthorize("hasAuthority('ADMIN')")
	public ResponseEntity<GuidedTour> updateTour(@RequestBody GuidedTour tour) {
		GuidedTour guidedTour=this.tourService.updateTour(tour);
		if(guidedTour!=null) {
			return new ResponseEntity<GuidedTour>(guidedTour,HttpStatus.OK);
		}
		return new ResponseEntity<GuidedTour>(HttpStatus.NOT_MODIFIED);
		 
	}

	@DeleteMapping("/{id}")
	@PreAuthorize("hasAuthority('ADMIN')")
	public ResponseEntity<HttpStatus> deleteTour(@PathVariable Long id) {
		if (tourService.deleteTourById(id) == true) {
			return new ResponseEntity<HttpStatus>(HttpStatus.OK);
		}
		return new ResponseEntity<HttpStatus>(HttpStatus.NOT_ACCEPTABLE); 
	}

	
}


```

```java title="UserController.java"
package com.jt.controller;

import java.util.List;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.http.HttpStatus;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RequestMapping;
import org.springframework.web.bind.annotation.RestController;

import com.jt.model.auth.User;
import com.jt.service.UserService;

@RequestMapping("/users")
@RestController
public class UserController {
	@Autowired
	private UserService service;
	
	@PostMapping()
	public ResponseEntity<User> addUser(@RequestBody User user) throws Exception {
		User addUser=this.service.createTheUser(user);
		if(addUser!=null) {
			return new ResponseEntity<User>(addUser,HttpStatus.CREATED);
		}
		return new ResponseEntity<User>(addUser,HttpStatus.NOT_ACCEPTABLE);
	}
	@GetMapping()
	public ResponseEntity<List<User>> getUsers() {
		List<User> users=this.service.getAllTheUsers();
		if(users!=null) {
			return new ResponseEntity<List<User>>(users,HttpStatus.OK);
		}
		return new ResponseEntity<List<User>>(users,HttpStatus.NOT_FOUND);
		
	}
	
	
}


```
