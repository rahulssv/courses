# Repository

```java title="BatchRepository.java"
package com.jt.repository;

import java.util.Date;
import java.util.List;

import org.springframework.data.jpa.repository.Modifying;
import org.springframework.data.jpa.repository.Query;
import org.springframework.data.repository.CrudRepository;
import org.springframework.data.repository.query.Param;

import com.jt.model.batch.Status;
import com.jt.model.batch.TourBatch;

import jakarta.transaction.Transactional;

public interface BatchRepository extends CrudRepository<TourBatch, Long> {

	List<TourBatch> findAllByTourId(Long tourId);
	@Query(value = "select * from Tour_Batch where TOUR_BATCH.START_DATE >=:minDate AND TOUR_BATCH.START_DATE <=:maxDate", nativeQuery = true)
	List<TourBatch> findBatchesBetween(@Param("minDate") Date minDate, @Param("maxDate") Date maxDate);

	@Query(value = "select * from Tour_Batch  where TOUR_BATCH.START_DATE >=:minDate", nativeQuery = true)
	List<TourBatch> findBatchesAfter(@Param("minDate") Date minDate);
	
	@Query(value = "select * from Tour_Batch  where TOUR_BATCH.START_DATE <=:maxDate", nativeQuery = true)
	List<TourBatch> findBatchesBefore(@Param("maxDate") Date maxDate);
	
	List<TourBatch> findAllByTourIdAndStatus(Long tourId,Status status) ;
	
	List<TourBatch> findAllByStatus(Status status) ;
	
	@Transactional
	@Modifying
	@Query("UPDATE TourBatch t "
			+ "SET t.status = "
			+ "CASE "
			+ "WHEN t.availableSeats = t.capacity THEN 'CANCELLED' "
			+ "WHEN CURRENT_DATE() > t.endDate THEN 'COMPLETED' "
			+ "WHEN t.availableSeats < t.capacity THEN 'IN_PROGRESS' "
			+ "END "
			+ "WHERE CURRENT_DATE() > t.startDate")
	void updateStatus();
	
	@Query("SELECT r from TourBatch r WHERE r.status = :status")
	List<TourBatch> findBatchByStatus(@Param("status") Status status);
	
	@Query("SELECT r from TourBatch r WHERE r.availableSeats >= :minAvailableSeats AND r.availableSeats <= :maxAvailableSeats")
	List<TourBatch> findFilteredAvailableSeats(@Param("minAvailableSeats") int minAvailableSeats, @Param("maxAvailableSeats") int maxAvailableSeats);

	@Query("SELECT r from TourBatch r WHERE r.availableSeats >= :minAvailableSeats")
	List<TourBatch> findMinAvailableSeats(@Param("minAvailableSeats") int minAvailableSeats);
	
	@Query("SELECT r from TourBatch r WHERE r.availableSeats <= :maxAvailableSeats")
	List<TourBatch> findMaxAvailableSeats(@Param("maxAvailableSeats") int maxAvailableSeats);
	
	@Query("SELECT r from TourBatch r WHERE r.perParticipantCost <= :budget")
	List<TourBatch> findFilteredPrice(@Param("budget") double budget);
}

```
```java title="BookingRepository.java"
package com.jt.repository;

import java.util.List;

import org.springframework.data.repository.CrudRepository;

import com.jt.model.batch.Booking;

public interface BookingRepository extends CrudRepository<Booking, Long>{
	
	List<Booking> findAllByUsername(String username);

	List<Booking> findAllByBatchId(Long id);

}

```
```java title="MetadataRepository.java"
package com.jt.repository;

public interface MetadataRepository {

}

```
```java title="TourRepository.java"
package com.jt.repository;

import java.util.List;

import org.springframework.data.jpa.repository.Query;
import org.springframework.data.repository.CrudRepository;
import org.springframework.data.repository.query.Param;
import org.springframework.stereotype.Repository;

import com.jt.model.tour.DifficultyLevel;
import com.jt.model.tour.GuidedTour;
import com.jt.model.tour.Mode;

@Repository
public interface TourRepository extends CrudRepository<GuidedTour, Long> {
	@Query("SELECT r from GuidedTour r WHERE r.days >= :minDays AND r.days <= :maxDays")
	List<GuidedTour> filterTourByDuration(@Param("minDays") int minDays, @Param("maxDays") int maxDays);

	@Query("SELECT r from GuidedTour r WHERE r.startAt = :source AND r.endAt = :destination")
	List<GuidedTour> filterToursByPlaceBetween(@Param("source") String source,
			@Param("destination") String destination);

	@Query("SELECT r from GuidedTour r WHERE r.startAt = :source")
	List<GuidedTour> filterToursByPlaceSource(@Param("source") String source);

	@Query("SELECT r from GuidedTour r WHERE r.endAt = :destination")
	List<GuidedTour> filterToursByPlaceDestination(@Param("destination") String destination);

	@Query("SELECT r from GuidedTour r WHERE r.mode = :mode")
	List<GuidedTour> filterToursByMode(@Param("mode") Mode mode);

	@Query("SELECT r from GuidedTour r WHERE r.difficultyLevel = :difficultyLevel")
	List<GuidedTour> filteredToursByDifficultyLevel(@Param("difficultyLevel") DifficultyLevel difficultyLevel);

	@Query(value = "SELECT t.* FROM guided_tour t " + "JOIN (SELECT tour_id, MAX(batch_completed) AS max_completed "
			+ "FROM (SELECT tb.tour_id, COUNT(*) AS batch_completed "
			+ "FROM tour_batch tb WHERE tb.status = 'COMPLETED' GROUP BY tb.tour_id) AS batches "
			+ "GROUP BY tour_id) AS max_batches " + "ON t.id = max_batches.tour_id "
			+ "ORDER BY max_batches.max_completed DESC " + "LIMIT 3", nativeQuery = true)
	List<GuidedTour> findMostPopularTours();
}

```
```java title="UserRepository.java"
package com.jt.repository;

import java.util.Optional;

import org.springframework.data.repository.CrudRepository;
import org.springframework.stereotype.Repository;

import com.jt.model.auth.Role;
import com.jt.model.auth.User;

@Repository
public interface UserRepository extends CrudRepository<User, String> {
	User findByRole(Role role) ;
	Optional<User> findByUserName(String email) ;
}

```
