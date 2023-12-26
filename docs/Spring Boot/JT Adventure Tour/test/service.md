# Service Test
```java title="BookingServiceTest.java"
package com.jt.service;

import static org.assertj.core.api.Assertions.assertThat;

import java.util.Arrays;
import java.util.List;
import java.util.Optional;

import org.junit.jupiter.api.DisplayName;
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.extension.ExtendWith;
import org.mockito.InjectMocks;
import org.mockito.Mock;
import org.mockito.Mockito;
import org.mockito.junit.jupiter.MockitoExtension;
import com.jt.controller.BatchControllerTest;
import com.jt.controller.BookingControllerTest;
import com.jt.model.batch.Booking;
import com.jt.model.batch.TourBatch;
import com.jt.repository.BatchRepository;
import com.jt.repository.BookingRepository;
import jakarta.persistence.EntityNotFoundException;

@ExtendWith(MockitoExtension.class)
@DisplayName("TourBatchService Testing")
public class BookingServiceTest {

	@Mock
	private BookingRepository bookingRepository;
	
	@Mock
	private BatchRepository batchRepository;
	
	@InjectMocks
	private BookingService bookingService;
	
	@InjectMocks
	private BatchService batchService;
	
	
	Booking book = BookingControllerTest.dummyBookingData();
	TourBatch batch = BatchControllerTest.getDummyDataTourBatch();
	@Test
	@DisplayName("Testing booking service addBook inside batchService")
	public void bookTravellerTest() {
		Mockito.when(bookingRepository.save(book)).thenReturn(book);
		Mockito.when(batchRepository.findById(Mockito.anyLong())).thenReturn(Optional.of(batch));
		Mockito.when(batchRepository.save(batch)).thenReturn(batch);
		Mockito.when(bookingRepository.findAllByBatchId(book.getBatchId())).thenReturn(Arrays.asList(book));
		Booking bookResponse = batchService.bookTraveller(book);
		assertThat(bookResponse).isNotNull();
	}
	@Test
	@DisplayName("Testing booking service addBook inside batchService")
	public void bookTravellerTestForException() {
		Mockito.when(batchRepository.findById(Mockito.anyLong())).thenThrow(new EntityNotFoundException("batch not found for these booking"));
		Booking bookResponse = batchService.bookTraveller(book);
		assertThat(bookResponse).isNull();
	}
	@Test
	@DisplayName("Testing get all booking service")
	public void GetBookingsTest() {
		Mockito.when(bookingRepository.findAll()).thenReturn(Arrays.asList(book));
		
		List<Booking> bookResponse = bookingService.getAllBookings();
		
		assertThat(bookResponse).isNotEmpty();
	}
	@Test
	@DisplayName("Testing get all booking service for Exception")
	public void GetBookingsTestForInvalid() throws EntityNotFoundException{
		Mockito.when(bookingRepository.findAll()).thenThrow(new EntityNotFoundException("invalid case"));
		List<Booking> bookResponse = bookingService.getAllBookings();
		assertThat(bookResponse).isNull();
	}
	 @Test
	    @DisplayName("Testing get all bookings for a user")
	    public void getAllBookingsUserTest() {
	        // Arrange
	        String username = "testUser";
	        List<Booking> expectedBookings = Arrays.asList(book);
	 
	        Mockito.when(bookingRepository.findAllByUsername(username)).thenReturn(expectedBookings);
	        List<Booking> actualBookings = bookingService.getAllBookingsUser(username);
	        assertThat(actualBookings).isNotNull();
	        assertThat(actualBookings).isEqualTo(expectedBookings);
	    }
	 
	    @Test
	    @DisplayName("Testing get all bookings for a user when an exception occurs")
	    public void getAllBookingsUserTestForException() {
	        String username = "testUser";
	        Mockito.when(bookingRepository.findAllByUsername(username)).thenThrow(new RuntimeException("Test exception"));
	        List<Booking> actualBookings = bookingService.getAllBookingsUser(username);
	        assertThat(actualBookings).isNull();
	    }
}

```
```java title="TourBatchServiceTest.java"
package com.jt.service;

import static org.assertj.core.api.Assertions.assertThat;
import static org.junit.jupiter.api.Assertions.assertEquals;
import static org.junit.jupiter.api.Assertions.assertFalse;
import static org.junit.jupiter.api.Assertions.assertTrue;
import static org.mockito.Mockito.when;

import java.text.ParseException;
import java.text.SimpleDateFormat;
import java.util.ArrayList;
import java.util.Date;
import java.util.List;
import java.util.Optional;

import org.junit.jupiter.api.DisplayName;
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.extension.ExtendWith;
import org.mockito.InjectMocks;
import org.mockito.Mock;
import org.mockito.Mockito;
import org.mockito.junit.jupiter.MockitoExtension;

import com.jt.controller.BatchControllerTest;
import com.jt.controller.TourControllerTest;
import com.jt.model.batch.Status;
import com.jt.model.batch.TourBatch;
import com.jt.model.tour.GuidedTour;
import com.jt.repository.TourRepository;

import jakarta.persistence.EntityNotFoundException;

import com.jt.repository.BatchRepository;


@ExtendWith(MockitoExtension.class)
@DisplayName("TourBatchService Testing")
public class TourBatchServiceTest {
	
	@Mock
	private BatchRepository batchRepository;
	
	@Mock
	private TourRepository guidedTourRepository;
	
	@InjectMocks
	private BatchService tourBatchServiceImpl;
	
	TourBatch tourBatch = BatchControllerTest.getDummyDataTourBatch();
	TourBatch tourBatch2 = TourControllerTest.dummyDataForBatch();
	GuidedTour guidedTour = TourControllerTest.dummyDataForTour();
	
	@Test
	@DisplayName("Adding Tour Batch")
	public void addBatchTest() throws Exception{
		Mockito.when(batchRepository.save(tourBatch)).thenReturn(tourBatch);
		Mockito.when(guidedTourRepository.findById(1l)).thenReturn(Optional.of(guidedTour));
		tourBatch.setEndDate(guidedTour.getDays());
		int bookedSeats = 0;
		tourBatch.setAvailableSeats(bookedSeats);
		tourBatch.setStatus("Active");
		tourBatch.getGuide().setBookingSequence(0);;
		System.out.println("tourbatchresponse "+tourBatch);
		TourBatch tourBatchResponse = tourBatchServiceImpl.addBatch(1L, tourBatch);
		System.out.println("tourbatchresponse "+tourBatchResponse);
		assertThat(tourBatchResponse).isNotNull();
		
	}
	@Test
	@DisplayName("Adding Tour Batch for empty batch object")
	public void addBatchTestNotNull() throws Exception{
		Mockito.when(batchRepository.save(tourBatch)).thenThrow(new EntityNotFoundException("Batch Object is empty"));
		Mockito.when(guidedTourRepository.findById(1l)).thenReturn(Optional.of(guidedTour));
		TourBatch tourBatchResponse = tourBatchServiceImpl.addBatch(1L, tourBatch);
		assertThat(tourBatchResponse).isNull();
		
	}
	@Test
	@DisplayName("Get tour Batches")
	public void getBatches()throws Exception {
		List<TourBatch> listOfBatches = new ArrayList<>();
		listOfBatches.add(tourBatch);
		Mockito.when(batchRepository.findAll()).thenReturn(listOfBatches);
		List<TourBatch> response = tourBatchServiceImpl.getBatches();
		assertThat(response).isNotEmpty();
	}
	@Test
	@DisplayName("Get tour Batches for invalid batches")
	public void getBatchesForInvalidTest()throws Exception {
		List<TourBatch> listOfBatches = new ArrayList<>();
		listOfBatches.add(tourBatch);
		Mockito.when(batchRepository.findAll()).thenThrow(new EntityNotFoundException("no object found for batches"));
		List<TourBatch> response = tourBatchServiceImpl.getBatches();
		assertThat(response).isNull();
	}

	@Test
	@DisplayName("Get Batch By Id")
	public void getBatchById() {
		Mockito.when(batchRepository.findById(1l)).thenReturn(Optional.of(tourBatch));
		TourBatch response = tourBatchServiceImpl.getBatchById(1l);
		assertThat(response).isNotNull();
		assertEquals(response.getCapacity(), 55);

	}
	@Test
	@DisplayName("Get Batch By Id for Invalid id")
	public void getBatchByIdForInvalidId() {
		Mockito.when(batchRepository.findById(1l)).thenReturn(Optional.empty());
		TourBatch response = tourBatchServiceImpl.getBatchById(1l);
		assertThat(response).isNull();

	}
	@Test
	@DisplayName("Delete Batch by id")
	public void deleteBatchById() throws Exception{
		Mockito.when(batchRepository.findById(1l)).thenReturn(Optional.of(tourBatch));
		Mockito.when(batchRepository.save(tourBatch)).thenReturn(tourBatch);
		boolean response = tourBatchServiceImpl.deleteBatchById(1l);
		assertTrue(response);
	}
	@Test()
	@DisplayName("Delete Batch by id for Invalid Id")
	public void deleteBatchByIdForInvalidId() {
		when(batchRepository.findById(1l)).thenReturn(Optional.empty());
		boolean response = tourBatchServiceImpl.deleteBatchById(1l);
		assertFalse(response);	
	}
	
	@Test
	@DisplayName("Update Batch")
	public void updateBatch()throws Exception {

		tourBatch2.setCapacity(55);
		Mockito.when(batchRepository.findById(1l)).thenReturn(Optional.of(tourBatch2));
		Mockito.when(batchRepository.save(tourBatch2)).thenReturn(tourBatch2);
		tourBatch.setAvailableSeats(tourBatch2.getCapacity() - tourBatch2.getAvailableSeats());
		TourBatch tourBatchResponse = tourBatchServiceImpl.updateBatch(tourBatch2);
		System.out.println(tourBatchResponse);
		assertThat(tourBatchResponse).isNotNull();
		assertThat(tourBatchResponse.getCapacity()).isEqualTo(55);
		
	}
	
	@Test
	@DisplayName("Test Filter")
	public void getFilterBatches() throws ParseException {
		String min_String= "26-09-2023";
		String max_String = "30-09-2023";
	    SimpleDateFormat formatter = new SimpleDateFormat("dd-MM-yyyy");      
	    Date minDate = formatter.parse(min_String); 
	    Date maxDate = formatter.parse(max_String);
	    List<TourBatch> listOfTourBatch = new ArrayList<>();
	    listOfTourBatch.add(tourBatch);
	    when(batchRepository.findBatchesBetween(minDate, maxDate)).thenReturn(listOfTourBatch);
		List<TourBatch> result = tourBatchServiceImpl.getFilteredBatches(minDate, maxDate);
		assertThat(result).isNotEmpty();
				
	}
	
	@Test
	@DisplayName("Test Filter")
	public void getFilterBatchesforMinDateMaxDateInvalid() throws ParseException {
		String min_String= "30-09-2023";
		String max_String = "26-09-2023";
	    SimpleDateFormat formatter = new SimpleDateFormat("dd-MM-yyyy");      
	    Date minDate = formatter.parse(min_String); 
	    Date maxDate = formatter.parse(max_String);
	    List<TourBatch> listOfTourBatch = new ArrayList<>();
	    listOfTourBatch.add(tourBatch);
		List<TourBatch> result = tourBatchServiceImpl.getFilteredBatches(minDate, maxDate);
		assertThat(result).isNull();
				
	}
	
	@Test
	@DisplayName("Test Filter for Min Date is null")
	public void getFilterBatchesMinDateNull() throws ParseException {
		String min_String= "26-09-2023";
		String max_String = null;
	    SimpleDateFormat formatter = new SimpleDateFormat("dd-MM-yyyy");      
	    Date minDate = formatter.parse(min_String); 
	    Date maxDate = null;
	    List<TourBatch> listOfTourBatch = new ArrayList<>();
	    listOfTourBatch.add(tourBatch);
	    when(batchRepository.findBatchesAfter(minDate)).thenReturn(listOfTourBatch);
		List<TourBatch> result = tourBatchServiceImpl.getFilteredBatches(minDate, maxDate);
		assertThat(result).isNotEmpty();
				
	}
	
	@Test
	@DisplayName("Test Filter for max Date is null")
	public void getFilterBatchesMaxDateNull() throws ParseException {
		String min_String= "30-09-2023";
		String max_String = null ;
	    SimpleDateFormat formatter = new SimpleDateFormat("dd-MM-yyyy");      
	    Date minDate = formatter.parse(min_String); 
	    Date maxDate = null;
	    List<TourBatch> listOfTourBatch = new ArrayList<>();
	    listOfTourBatch.add(tourBatch);
	    when(batchRepository.findBatchesAfter(minDate)).thenReturn(listOfTourBatch);
		List<TourBatch> result = tourBatchServiceImpl.getFilteredBatches(minDate, maxDate);
		assertThat(result).isNotEmpty();
				
	}
	@Test
	@DisplayName("Test Filter")
	public void getFilterBatchesForNull() throws ParseException {
		List<TourBatch> result = tourBatchServiceImpl.getFilteredBatches(null, null);
		assertThat(result).isNull();
				
	}
	@Test
	@DisplayName("get batch by user")
	public void getBatchesByUserTest() throws Exception{
		List<TourBatch> listOfTourbatch = new ArrayList<>();
		listOfTourbatch.add(tourBatch);
		Mockito.when(batchRepository.findAllByStatus(Status.ACTIVE)).thenReturn(listOfTourbatch);
		List<TourBatch> response = tourBatchServiceImpl.getBatchesByUser();
		assertThat(response).isNotEmpty();
	}
	@Test
	@DisplayName("get batch by tour id")
	public void getBatchesBytourId() throws Exception{
		GuidedTour guidedTourInput = guidedTour;
		List<TourBatch> listOfTourbatch = new ArrayList<>();
		listOfTourbatch.add(tourBatch);
		
		Mockito.when(guidedTourRepository.findById(1l)).thenReturn(Optional.of(guidedTourInput));
		Mockito.when(batchRepository.findAllByTourIdAndStatus(1l, Status.ACTIVE)).thenReturn(listOfTourbatch);
		List<TourBatch> response = tourBatchServiceImpl.getBatchesByTourIdByUser(1l);
		assertThat(response).isNotEmpty();
	}
	@Test
	@DisplayName("get batch by tour id")
	public void getBatchesBytourIdForNull() throws Exception{
		List<TourBatch> listOfTourbatch = new ArrayList<>();
		listOfTourbatch.add(tourBatch);
		Mockito.when(guidedTourRepository.findById(1l)).thenReturn(Optional.empty());
		List<TourBatch> response = tourBatchServiceImpl.getBatchesByTourIdByUser(1l);
		assertThat(response).isNull();
	}
	
	@Test
	@DisplayName("get filter status")
	public void getFilteredStatusTest() throws Exception{
		List<TourBatch> listOfTourbatch = new ArrayList<>();
		listOfTourbatch.add(tourBatch);
		Mockito.when(batchRepository.findBatchByStatus(Status.ACTIVE)).thenReturn(listOfTourbatch);
		List<TourBatch> response = tourBatchServiceImpl.getFilteredStatus(Status.ACTIVE);
		assertThat(response).isNotEmpty();
	}
	
	@Test
	@DisplayName("get filter status")
	public void getFilteredAvailableSeats() throws Exception{
		int minSeat = -1;
		int maxSeat = -1;
		List<TourBatch> response = tourBatchServiceImpl.getFilteredAvailableSeats(minSeat , maxSeat);
		assertThat(response).isNull();
	}
	@Test
	@DisplayName("get filter status")
	public void getFilteredAvailableSeatsForNullMinDate() throws Exception{
		int minSeat = -1;
		int maxSeat = 10;
		List<TourBatch> listOfTourbatch = new ArrayList<>();
		listOfTourbatch.add(tourBatch);
		Mockito.when(batchRepository.findMaxAvailableSeats(maxSeat)).thenReturn(listOfTourbatch);
		List<TourBatch> response = tourBatchServiceImpl.getFilteredAvailableSeats(minSeat , maxSeat);
		assertThat(response).isNotEmpty();
	}
	@Test
	@DisplayName("get filter status")
	public void getFilteredAvailableSeatsForNullMaxDate() throws Exception{
		int minSeat = 10;
		int maxSeat = -1;
		List<TourBatch> listOfTourbatch = new ArrayList<>();
		listOfTourbatch.add(tourBatch);
		Mockito.when(batchRepository.findMinAvailableSeats(minSeat)).thenReturn(listOfTourbatch);
		List<TourBatch> response = tourBatchServiceImpl.getFilteredAvailableSeats(minSeat , maxSeat);
		assertThat(response).isNotEmpty();
	}
	@Test
	@DisplayName("get filter status")
	public void getFilteredAvailableSeatsForNullminDateLessThanMax() throws Exception{
		int minSeat = 1;
		int maxSeat = 10;
		List<TourBatch> listOfTourbatch = new ArrayList<>();
		listOfTourbatch.add(tourBatch);
		Mockito.when(batchRepository.findFilteredAvailableSeats(minSeat , maxSeat)).thenReturn(listOfTourbatch);
		List<TourBatch> response = tourBatchServiceImpl.getFilteredAvailableSeats(minSeat , maxSeat);
		assertThat(response).isNotEmpty();
	}
	
	@Test
	@DisplayName("get filter status")
	public void getFilteredAvailableSeatsForNull() throws Exception{
		int minSeat = -1;
		int maxSeat = -1;
		List<TourBatch> listOfTourbatch = new ArrayList<>();
		listOfTourbatch.add(tourBatch);
		List<TourBatch> response = tourBatchServiceImpl.getFilteredAvailableSeats(minSeat , maxSeat);
		assertThat(response).isNull();
	}
	@Test
	@DisplayName("get filter status")
	public void getFilteredPriceForNull() throws Exception{
		double budget = -1;
		List<TourBatch> response = tourBatchServiceImpl.getFilteredPrice(budget);
		assertThat(response).isNull();
	}
	@Test
	@DisplayName("get filter status")
	public void getFilteredPrice() throws Exception{
		double budget = 1000;
		List<TourBatch> listOfTourbatch = new ArrayList<>();
		listOfTourbatch.add(tourBatch);
		Mockito.when(batchRepository.findFilteredPrice(budget)).thenReturn(listOfTourbatch);
		List<TourBatch> response = tourBatchServiceImpl.getFilteredPrice(budget);
		assertThat(response).isNotEmpty();
	}
	
}

```
```java title="TourServiceTest.java"
package com.jt.service;

import static org.assertj.core.api.Assertions.assertThat;
import static org.junit.jupiter.api.Assertions.assertEquals;
import static org.junit.jupiter.api.Assertions.assertFalse;
import static org.junit.jupiter.api.Assertions.assertTrue;
import static org.mockito.Mockito.verify;
import static org.mockito.Mockito.when;

import java.util.ArrayList;
import java.util.List;
import java.util.Optional;

import org.junit.jupiter.api.DisplayName;
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.extension.ExtendWith;
import org.mockito.InjectMocks;
import org.mockito.Mock;
import org.mockito.Mockito;
import org.mockito.Spy;
import org.mockito.junit.jupiter.MockitoExtension;

import com.jt.controller.TourControllerTest;
import com.jt.model.batch.TourBatch;
import com.jt.model.tour.DifficultyLevel;
import com.jt.model.tour.GuidedTour;
import com.jt.model.tour.Mode;
import com.jt.repository.BatchRepository;
import com.jt.repository.TourRepository;

import jakarta.persistence.EntityNotFoundException;


@ExtendWith(MockitoExtension.class)
@DisplayName("TourService Testing")
public class TourServiceTest {

	@Mock
	private TourRepository tourRepository;
	
	@Mock
	private BatchRepository tourBatchRepository;

	@InjectMocks
	@Spy
	private TourService tourService;
	
	GuidedTour guidedTour = TourControllerTest.dummyDataForTour();
	
	@Test
	@DisplayName("Testing TourService Create Tour")
	public void createTourTest() {
		Mockito.when(tourRepository.save(guidedTour)).thenReturn(guidedTour);
		GuidedTour guidedTourSaveObject = tourService.addTour(guidedTour);
		assertThat(guidedTourSaveObject).isNotNull();
	}
	@Test
	@DisplayName("Testing TourService Create Tour for Null")
	public void createTourTestForEmptyTour() {
		Mockito.when(tourRepository.save(guidedTour)).thenThrow(new EntityNotFoundException("not saving tour because null"));
		GuidedTour guidedTourSaveObject = tourService.addTour(guidedTour);
		assertThat(guidedTourSaveObject).isNull();
	}
	
	@Test
	@DisplayName("Test tourService GetAll tours")
	public void allToursTest() {
		List<GuidedTour> guidedTourList = new ArrayList<>();
		guidedTourList.add(guidedTour);
		Mockito.when(tourRepository.findAll()).thenReturn(guidedTourList);
		List<GuidedTour> responseList = tourService.getTours();
		assertThat(responseList).isNotNull();
		assertThat(responseList).isNotEmpty();
	}
	@Test
	@DisplayName("Test tourService GetAll tours Empty list")
	public void allToursTestForNull() {
		List<GuidedTour> guidedTourList = new ArrayList<>();
		guidedTourList.add(guidedTour);
		Mockito.when(tourRepository.findAll()).thenThrow(new EntityNotFoundException("Empty list of Tours"));
		List<GuidedTour> responseList = tourService.getTours();
		assertThat(responseList).isNull();
	}
	
	@Test
	@DisplayName("Test Tourservice TourById")
	public void tourByIdTest() {
		Optional<GuidedTour> optional = Optional.of(guidedTour);
		Mockito.when(tourRepository.findById(Mockito.anyLong())).thenReturn(optional);
		GuidedTour responseGuidedTour = tourService.getTourById(1l);
		assertThat(responseGuidedTour).isNotNull();
		assertEquals(responseGuidedTour.getName() , "mumbai-leh");	
	}
	
	@Test
	@DisplayName("Test Tourservice TourById for Invalid id")
	public void tourByIdTestForInvalidId() {
		Mockito.when(tourRepository.findById(Mockito.anyLong())).thenThrow(new EntityNotFoundException("not found with tour id"));
		GuidedTour responseGuidedTour = tourService.getTourById(1l);
		assertThat(responseGuidedTour).isNull();	
	}
	@Test
	@DisplayName("Test deleteById")
	public void deleteTourById() {
		Long tourId = 1L;
		Mockito.doNothing().when(tourRepository).deleteById(tourId);
		boolean result = tourService.deleteTourById(tourId);
		assertTrue(result);
	}
	@Test
	@DisplayName("Test deleteById for Invalid id")
	public void deleteTourByIdForInvalidId() {
		Long tourId = -1L;
		Mockito.doNothing().when(tourRepository).deleteById(0L);
		boolean result = tourService.deleteTourById(tourId);
		assertFalse(result);
	}
	
	@Test
	@DisplayName("Test update tour")
	public void updateTour () {
		Long tourId =1L;
		GuidedTour guidedTourInput = new GuidedTour();
		guidedTourInput.setId(tourId);
		guidedTourInput.setName("nagpur-goa");
		when(tourRepository.findById(tourId)).thenReturn(Optional.of(guidedTourInput));
		when(tourRepository.save(guidedTourInput)).thenReturn(guidedTourInput);
		GuidedTour result = tourService.updateTour(guidedTourInput);
		verify(tourRepository).save(guidedTourInput);
		assertThat(result).isNotNull();
	}
	@Test
	@DisplayName("Test update tour")
	public void updateTourForInvalidTour () {
		Long tourId =1L;
		GuidedTour guidedTourInput = new GuidedTour();
		guidedTourInput.setId(tourId);
		guidedTourInput.setName("nagpur-goa");
		when(tourRepository.findById(tourId)).thenThrow(new EntityNotFoundException("Update failed"));
		when(tourRepository.save(guidedTourInput)).thenReturn(guidedTourInput);
		GuidedTour result = tourService.updateTour(guidedTourInput);
		verify(tourRepository).save(guidedTourInput);
		assertThat(result).isNull();
	}
	@Test
	@DisplayName("Test get all tourbatch for tour")
	public void getTourBatches() {
		Long tourId = 1L;
		TourBatch tourBatch = new TourBatch();
		tourBatch.setId(tourId);
		List<TourBatch>listOfBatch = new ArrayList<>();
		listOfBatch.add(tourBatch);
		when(tourBatchRepository.findAllByTourId(tourId)).thenReturn(listOfBatch);
		List<TourBatch> result = tourService.getTourBatches(tourId);
		assertThat(result).isNotEmpty();
	}
	
	@Test
	@DisplayName("Test get all tourbatch for tour for invalid case")
	public void getTourBatchesForInvalidCase() {
		Long tourId = 1L;
		TourBatch tourBatch = new TourBatch();
		tourBatch.setId(tourId);
		List<TourBatch>listOfBatch = new ArrayList<>();
		listOfBatch.add(tourBatch);
		when(tourBatchRepository.findAllByTourId(tourId)).thenThrow(new EntityNotFoundException("No batch available for tour"));
		List<TourBatch> result = tourService.getTourBatches(tourId);
		assertThat(result).isNull();
	}
	
	@Test
	@DisplayName("filter tour by duration")
	public void filterTourByDuration() {
		int minDays = -1;
		int maxDays  = 10;
		List<GuidedTour> guidedToursList = new ArrayList<>();
		guidedToursList.add(guidedTour);
		Mockito.when(tourRepository.filterTourByDuration(minDays, maxDays)).thenReturn(guidedToursList);
		
		List<GuidedTour> response = tourService.filterTourByDuration(minDays, maxDays);
		assertThat(response).isNotEmpty();
	}
	
	@Test
	@DisplayName("filter tour by duration")
	public void filterTourByDurationForInvalidTest() {
		int minDays = 1;
		int maxDays  = -10;
		List<GuidedTour> guidedToursList = new ArrayList<>();
		guidedToursList.add(guidedTour);		
		List<GuidedTour> response = tourService.filterTourByDuration(minDays, maxDays);
		assertThat(response).isEmpty();
	}
	
	@Test
	@DisplayName("filter tour by Places")
	public void filterTourByPlace() {
		String source = "mumbai";
		String destination  = "leh";
		List<GuidedTour> guidedToursList = new ArrayList<>();
		guidedToursList.add(guidedTour);	
		
		Mockito.when(tourRepository.filterToursByPlaceBetween(source, destination)).thenReturn(guidedToursList);
		
		List<GuidedTour> response = tourService.filteredToursByPlace(source, destination);
		assertThat(response).isNotEmpty();
	}
	@Test
	@DisplayName("filter tour by Places for Null")
	public void filterTourByPlaceForNull() {
		String source = null;
		String destination  = null;
		List<GuidedTour> guidedToursList = new ArrayList<>();
		guidedToursList.add(guidedTour);	
		
		Mockito.when(tourRepository.findAll()).thenReturn(guidedToursList);
		
		List<GuidedTour> response = tourService.filteredToursByPlace(source, destination);
		assertThat(response).isNotEmpty();
	}
	@Test
	@DisplayName("filter tour by Places for Null")
	public void filterTourByPlaceForSourceNull() {
		String source = null;
		String destination  = "leh";
		List<GuidedTour> guidedToursList = new ArrayList<>();
		guidedToursList.add(guidedTour);	
		
		Mockito.when(tourRepository.filterToursByPlaceDestination(destination)).thenReturn(guidedToursList);
		
		List<GuidedTour> response = tourService.filteredToursByPlace(source, destination);
		assertThat(response).isNotEmpty();
	}
	@Test
	@DisplayName("filter tour by Places for Null")
	public void filterTourByPlaceForDestinationNull() {
		String source = "mumbai";
		String destination  = null;
		List<GuidedTour> guidedToursList = new ArrayList<>();
		guidedToursList.add(guidedTour);	
		
		Mockito.when(tourRepository.filterToursByPlaceSource(source)).thenReturn(guidedToursList);
		
		List<GuidedTour> response = tourService.filteredToursByPlace(source, destination);
		assertThat(response).isNotEmpty();
	}
	@Test
	@DisplayName("filter tour by Places for source and destination are equals")
	public void filterTourByPlaceForSourceAndDestinationEqualas() {
		String source = "mumbai";
		String destination  = "mumbai";
		List<GuidedTour> guidedToursList = new ArrayList<>();
		guidedToursList.add(guidedTour);		
		List<GuidedTour> response = tourService.filteredToursByPlace(source, destination);
		assertThat(response).isNull();
	}
	@Test
	@DisplayName("filter tour by Places for source and destination are equals")
	public void filteredToursByModeTest() {
		Mode mode = Mode.BICYCLE;
		List<GuidedTour> guidedToursList = new ArrayList<>();
		guidedToursList.add(guidedTour);	
		Mockito.when(tourRepository.filterToursByMode(mode)).thenReturn(guidedToursList);
		List<GuidedTour> response = tourService.filteredToursByMode(mode);
		assertThat(response).isNotEmpty();
	}
	@Test
	@DisplayName("filter tour by Places for source and destination are equals")
	public void filteredToursByModeTestForNull() {
		Mode mode = null;
		List<GuidedTour> guidedToursList = new ArrayList<>();
		guidedToursList.add(guidedTour);	
		Mockito.when(tourRepository.findAll()).thenReturn(guidedToursList);
		List<GuidedTour> response = tourService.filteredToursByMode(mode);
		assertThat(response).isNotEmpty();
	}
	@Test
	@DisplayName("filter tours by difficulty")
	public void filteredToursByDifficultyLevelTest() {
		DifficultyLevel diff = DifficultyLevel.EASY;
		List<GuidedTour> guidedToursList = new ArrayList<>();
		guidedToursList.add(guidedTour);	
		Mockito.when(tourRepository.filteredToursByDifficultyLevel(diff)).thenReturn(guidedToursList);
		List<GuidedTour> response = tourService.filteredToursByDifficultyLevel(diff);
		assertThat(response).isNotEmpty();
	}
	
	
}

```
```java title="UserServicesTest.java"
package com.jt.service;

import static org.assertj.core.api.Assertions.assertThat;
import static org.junit.jupiter.api.Assertions.assertEquals;
import static org.junit.jupiter.api.Assertions.assertNotNull;
import static org.mockito.Mockito.times;
import static org.mockito.Mockito.verify;
import static org.mockito.Mockito.when;

import org.junit.jupiter.api.DisplayName;
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.extension.ExtendWith;
import org.mockito.InjectMocks;
import org.mockito.Mock;
import org.mockito.junit.jupiter.MockitoExtension;

import org.springframework.security.crypto.password.PasswordEncoder;
import com.jt.controller.AuthController;
import com.jt.model.auth.Role;
import com.jt.model.auth.User;
import com.jt.repository.UserRepository;

@ExtendWith(MockitoExtension.class)
public class UserServicesTest {


	@Mock
	private UserRepository userRepo;

	@Mock
	private PasswordEncoder passwordEncoder;

	@InjectMocks
	private UserService userService;

	@InjectMocks
	private AuthController yourController;

	@Test
	@DisplayName("Test Add User as ADMIN")
	public void testAddUserAsAdmin() throws Exception {
		User user = new User();
		user.setRole(Role.ADMIN);
		user.setUserName("adminUser");
		user.setPassword("adminPassword");
        when(userRepo.findByRole(Role.valueOf("ADMIN"))).thenReturn(null);
		when(passwordEncoder.encode(user.getPassword())).thenReturn("encodedPassword");
		when(userRepo.save(user)).thenReturn(user);
		User result = userService.createTheUser(user);
		verify(userRepo, times(1)).save(user);
		assertNotNull(result);
		assertEquals(user, result);
	}
	
	@Test
	@DisplayName("Test Add User as ADMIN for null")
	public void testAddUserAsAdminForReturnNull() throws Exception {
		User user = new User();
		user.setRole(Role.ADMIN);
		user.setUserName("adminUser");
		user.setPassword("adminPassword");
        when(userRepo.findByRole(Role.valueOf("ADMIN"))).thenReturn(user);	
		User result = userService.createTheUser(user);
		assertThat(result).isNull();
	}
}

```
