# Controller Test
```java title="AuthControllerTest.java"
package com.jt.controller;

import static org.hamcrest.CoreMatchers.is;
import static org.mockito.Mockito.when;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.jsonPath;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.status;
import java.util.Optional;
import org.springframework.security.core.Authentication;
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.DisplayName;
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.extension.ExtendWith;
import org.mockito.InjectMocks;
import org.mockito.Mock;
import org.mockito.Mockito;
import org.mockito.junit.jupiter.MockitoExtension;
import org.springframework.http.MediaType;
import org.springframework.security.authentication.AuthenticationManager;
import org.springframework.security.authentication.UsernamePasswordAuthenticationToken;
import org.springframework.test.web.servlet.MockMvc;
import org.springframework.test.web.servlet.request.MockHttpServletRequestBuilder;
import org.springframework.test.web.servlet.request.MockMvcRequestBuilders;
import org.springframework.test.web.servlet.setup.MockMvcBuilders;
import com.fasterxml.jackson.databind.ObjectMapper;
import com.fasterxml.jackson.databind.ObjectWriter;
import com.jt.auth.AuthRequest;
import com.jt.auth.AuthResponse;
import com.jt.model.auth.Role;
import com.jt.model.auth.User;
import com.jt.repository.UserRepository;
import com.jt.service.JwtService;
import com.jt.service.UserService;

@ExtendWith(MockitoExtension.class)
@DisplayName("AuthController Testing")
public class AuthControllerTest {

private MockMvc mockMvc;
	
	ObjectMapper objectMapper = new ObjectMapper();
	ObjectWriter objectIdWriter = objectMapper.writer();

	@Mock
	private UserService userService;
	
	@Mock
	private JwtService jwtService;
	
	@Mock
	private UserRepository userRepository;
	
	@Mock
	private AuthenticationManager authenticationManager;
	
	@InjectMocks
	private AuthController authController;
	
	@BeforeEach
	public void setUp() {
		this.mockMvc = MockMvcBuilders.standaloneSetup(authController).build();
	}
	
	public static User dummuyUser() {
		User user = new User();
		user.setUserName("harsh@gmail.com");
		user.setPassword("harsh");
		user.setRole(Role.CUSTOMER);
		return user;
	}
	public static AuthRequest dummyAuthRequest() {
		AuthRequest authRequest = new AuthRequest();
		authRequest.setUserName("harsh@gmail.com");
		authRequest.setPassword("harsh");
		return authRequest;
	}
	@Test
	@DisplayName("Testing register")
	public void createUserTest() throws Exception {
		User user = this.dummuyUser();
//		Mockito.when(userService.addUser(user)).thenReturn(this.dummuyUser());
		when(userService.createTheUser(user)).thenReturn(user);
		
		String content  = objectIdWriter.writeValueAsString(user);
		MockHttpServletRequestBuilder mockRequestBuilder = MockMvcRequestBuilders.post("/auth/register")
				.contentType(MediaType.APPLICATION_JSON)
				.accept(MediaType.APPLICATION_JSON)
				.content(content);
		
		mockMvc.perform(mockRequestBuilder)
				.andExpect(status().isCreated());

	}
	@Test
	@DisplayName("Testing register of empty user")
	public void createUserTestForIvalid() throws Exception {
		User user = null;
		String contentInput  = objectIdWriter.writeValueAsString(user);
		MockHttpServletRequestBuilder mockRequestBuilder = MockMvcRequestBuilders.post("/auth/register")
				.contentType(MediaType.APPLICATION_JSON)
				.accept(MediaType.APPLICATION_JSON)
				.content(contentInput);
		
		mockMvc.perform(mockRequestBuilder)
				.andExpect(status().isBadRequest());

	}
	
	@Test
	@DisplayName("Testing login test")
	public void authenticateAndGetTokenTest() throws Exception {
		AuthRequest authRequest = this.dummyAuthRequest();
		User user = this.dummuyUser();
		
		AuthResponse authResponse = new AuthResponse();
		authResponse.setToken("jwtToken");
		
		Authentication authentication = Mockito.mock(Authentication.class);
		
		when(authenticationManager.authenticate(new UsernamePasswordAuthenticationToken(authRequest.getUserName(), authRequest.getPassword())))
		.thenReturn(authentication);
		
		when(jwtService.generateToken(authRequest.getUserName())).thenReturn("MockedJwtString");
		
		when(authentication.isAuthenticated()).thenReturn(true);
		String content = objectIdWriter.writeValueAsString(authRequest);
		
		when(userRepository.findByUserName(user.getUserName())).thenReturn(Optional.of(user));
		MockHttpServletRequestBuilder mockRequestBuilder = MockMvcRequestBuilders.post("/auth/login")
				.contentType(MediaType.APPLICATION_JSON)
				.accept(MediaType.APPLICATION_JSON)
				.content(content);
		
		mockMvc.perform(mockRequestBuilder)
				.andExpect(jsonPath("$.token", is("MockedJwtString")));

	}
	
	@Test
    @DisplayName("Testing login test for invalid credentials")
    public void authenticateAndGetTokenTestForInvalid() throws Exception {
        AuthRequest authRequest = this.dummyAuthRequest();

        Authentication authentication = Mockito.mock(Authentication.class);

        when(authenticationManager.authenticate(new UsernamePasswordAuthenticationToken(authRequest.getUserName(), authRequest.getPassword())))
                .thenReturn(authentication);

        when(authentication.isAuthenticated()).thenReturn(false);

        String content = objectIdWriter.writeValueAsString(authRequest);
        try {
        	 mockMvc.perform(MockMvcRequestBuilders.post("/auth/login")
                     .contentType(MediaType.APPLICATION_JSON)
                     .content(content))
                     .andExpect(status().isOk())
                     .andExpect(jsonPath("$.error").value("UsernameNotFoundException"))
                     .andExpect(jsonPath("$.message").value("invalid user request"));
        	
        }catch(Exception e) {
        	e.printStackTrace();
        }
       
    }
}

```
```java title="BatchControllerTest.java"
package com.jt.controller;

import static org.hamcrest.CoreMatchers.is;
import static org.hamcrest.Matchers.hasSize;
import static org.hamcrest.Matchers.notNullValue;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.jsonPath;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.status;

import java.io.UnsupportedEncodingException;
import java.time.LocalDate;
import java.util.ArrayList;
import java.util.Arrays;
import java.util.Date;
import java.util.List;
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Disabled;
import org.junit.jupiter.api.DisplayName;
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.extension.ExtendWith;
import org.mockito.InjectMocks;
import org.mockito.Mock;
import org.mockito.Mockito;
import org.mockito.junit.jupiter.MockitoExtension;
import org.springframework.http.MediaType;
import org.springframework.test.web.servlet.MockMvc;
import org.springframework.test.web.servlet.request.MockHttpServletRequestBuilder;
import org.springframework.test.web.servlet.request.MockMvcRequestBuilders;
import org.springframework.test.web.servlet.setup.MockMvcBuilders;

import com.fasterxml.jackson.databind.ObjectMapper;
import com.fasterxml.jackson.datatype.jsr310.JavaTimeModule;

import com.fasterxml.jackson.databind.ObjectWriter;
import com.fasterxml.jackson.databind.json.JsonMapper;
import com.jt.model.batch.Booking;
import com.jt.model.batch.Status;
import com.jt.model.batch.TourBatch;
import com.jt.model.tour.GuidedTour;
import com.jt.model.user.MobileNumber;
import com.jt.model.user.Name;
import com.jt.model.user.Traveller;
import com.jt.service.BatchService;

@ExtendWith(MockitoExtension.class)
@DisplayName("BatchController Testing")
public class BatchControllerTest {
	
	private MockMvc mockMvc;

	ObjectMapper objectMapper = JsonMapper.builder()
            .addModule(new JavaTimeModule())
            .build();;
	ObjectWriter objectIdWriter = objectMapper.writer();
	
	@Mock
	private BatchService tourBatchService;

	@InjectMocks
	private BatchController tourBatchController;

	public static TourBatch getDummyDataTourBatch() {
		LocalDate date=LocalDate.now();
		TourBatch tb = new TourBatch();
		GuidedTour gt = new GuidedTour();
		Traveller tv=new Traveller();
		MobileNumber mn=new MobileNumber();
		mn.setNumber("9234567899");
		Name name=new Name();
		name.setFirst("harsh");
		name.setLast("last");
		
		tv.setMobile(mn);
		tv.setName(name);
		tv.setBookingSequence(0);
		
		gt.setId(1L);
		
		tb.setId(33L);
		tb.setStartDate(date);
		tb.setCapacity(55);
		tb.setPerParticipantCost(300d);
		tb.setEndDate(5);
		tb.setStatus(Status.ACTIVE.toString());
		tb.setGuide(tv);
		tb.setTour(TourControllerTest.dummyDataForTour());
		tb.setAvailableSeats(20);
		return tb;
	}
	
	public static Booking dummyBookingData() {
		Booking booking = new Booking();
		Date date = new Date();
//		Traveller traveller = new Traveller(1, new Name("harsh", "fulzele"), new MobileNumber("1234567890"));
		Traveller traveller = new Traveller();
		traveller.setBookingSequence(1);
		traveller.setMobile(new MobileNumber("9022018440"));
		traveller.setName(new Name("harsh" ,"fulzele"));
	
		booking.setId(1l);
		booking.setBatchId(1l);
		booking.setDate(date);
		booking.setAmount(12000.0);
		booking.setUsername("harsh@gmail.com");
		booking.setTravellers(Arrays.asList(traveller));
		return booking;
	}

	@BeforeEach
	public void setUp() {
		this.mockMvc = MockMvcBuilders.standaloneSetup(tourBatchController).build();
	}
	@Test
	@DisplayName("Testing Add book test")
	public void AddBookingTest() throws UnsupportedEncodingException, Exception {
		
		Booking book = this.dummyBookingData();
		System.out.println(book);
		Mockito.when(tourBatchService.bookTraveller(Mockito.any(Booking.class))).thenReturn(book);
		
		String content = objectIdWriter.writeValueAsString(this.dummyBookingData());
		
		MockHttpServletRequestBuilder mockRequestBuilder = MockMvcRequestBuilders.post("/batches/book")
				.contentType(MediaType.APPLICATION_JSON)
				.accept(MediaType.APPLICATION_JSON)
				.content(content);
		
		mockMvc.perform(mockRequestBuilder)
		.andExpect(status().isCreated())
		.andExpect(jsonPath("$", notNullValue()))
		.andReturn().getResponse().getContentAsString();

	}
	
	@Test
	@DisplayName("Testing Add book test for not Acceptable test")
	public void AddBookingTestForInvalidTest() throws UnsupportedEncodingException, Exception {
		
		Mockito.when(tourBatchService.bookTraveller(Mockito.any(Booking.class))).thenReturn(null);
		
		String content = objectIdWriter.writeValueAsString(this.dummyBookingData());
		
		MockHttpServletRequestBuilder mockRequestBuilder = MockMvcRequestBuilders.post("/batches/book")
				.contentType(MediaType.APPLICATION_JSON)
				.accept(MediaType.APPLICATION_JSON)
				.content(content);
		
		mockMvc.perform(mockRequestBuilder)
		.andExpect(status().isNotAcceptable());

	}
	@Disabled
	@Test
	@DisplayName("Test for getting all tour batches")
	public void getAllTourBatchesTest() throws UnsupportedEncodingException, Exception {
		
		List<TourBatch> tbList = new ArrayList<>();
		tbList.add(BatchControllerTest.getDummyDataTourBatch());

		Mockito.when(tourBatchService.getBatches()).thenReturn(tbList);

		mockMvc.perform(MockMvcRequestBuilders.get("/batches").contentType(MediaType.APPLICATION_JSON))
				.andExpect(status().isOk())
				.andExpect(jsonPath("$", notNullValue()))
				.andExpect(jsonPath("$", hasSize(1)))
				.andExpect(jsonPath("$[0].id", is(33)))
				.andReturn().getResponse().getContentAsString();
	}
	@Disabled
	@Test
	@DisplayName("Test for getting all tour batches")
	public void getAllTourBatchesTestForEmptyList() throws UnsupportedEncodingException, Exception {
		
		List<TourBatch> tbList = new ArrayList<>();
		tbList.add(BatchControllerTest.getDummyDataTourBatch());

		Mockito.when(tourBatchService.getBatches()).thenReturn(null);

		mockMvc.perform(MockMvcRequestBuilders.get("/batches")
				.contentType(MediaType.APPLICATION_JSON))
				.andExpect(status().isNotFound())
				.andExpect(jsonPath("$").doesNotExist());
	}

	@Test
	@DisplayName("Test for getting batch by id")
	public void getTourBatchByIdTest() throws Exception {
		Mockito.when(tourBatchService.getBatchById(33L)).thenReturn(BatchControllerTest.getDummyDataTourBatch());

		mockMvc.perform(MockMvcRequestBuilders.get("/batches/33").contentType(MediaType.APPLICATION_JSON))
				.andExpect(status().isFound())
				.andExpect(jsonPath("$", notNullValue()))
				.andExpect(jsonPath("$.id", is(33)))
				.andReturn().getResponse().getContentAsString();
	}
	
	@Test
	@DisplayName("Test for getting batch by id for Invalid Id")
	public void getTourBatchByIdTestForInvalidId() throws Exception {
		Mockito.when(tourBatchService.getBatchById(33L)).thenReturn(null);

		mockMvc.perform(MockMvcRequestBuilders.get("/batches/33").contentType(MediaType.APPLICATION_JSON))
				.andExpect(status().isNotFound())
				.andExpect(jsonPath("$").doesNotExist());
	}

	@Test
	@DisplayName("Test for updating tour batch")
	public void updateTourBatchTest() throws Exception {
		TourBatch tb = BatchControllerTest.getDummyDataTourBatch();
		tb.setCapacity(99);
		Mockito.when(tourBatchService.updateBatch(Mockito.any(TourBatch.class))).thenReturn(tb);
		String content = objectIdWriter.writeValueAsString(tb);
		MockHttpServletRequestBuilder mockRequestBuilder = MockMvcRequestBuilders.put("/batches")
				.contentType(MediaType.APPLICATION_JSON)
				.accept(MediaType.APPLICATION_JSON)
				.content(content);
		mockMvc.perform(mockRequestBuilder)
				.andExpect(status().isOk())
				.andExpect(jsonPath("$.capacity", is(99)))
				.andReturn().getResponse().getContentAsString();
	}
	@Test
	@DisplayName("Test for updating tour batch")
	public void updateTourBatchTestForInvalidStatus() throws Exception {
		TourBatch tb = BatchControllerTest.getDummyDataTourBatch();
		tb.setCapacity(99);
		Mockito.when(tourBatchService.updateBatch(Mockito.any(TourBatch.class))).thenReturn(null);
		String content = objectIdWriter.writeValueAsString(tb);
		MockHttpServletRequestBuilder mockRequestBuilder = MockMvcRequestBuilders.put("/batches")
				.contentType(MediaType.APPLICATION_JSON)
				.accept(MediaType.APPLICATION_JSON)
				.content(content);
		mockMvc.perform(mockRequestBuilder)
				.andExpect(status().isNotModified());
	}

	@Test
	@DisplayName("Test for deleting tour batch")
	public void deleteTourBatchTest() throws Exception {
		Mockito.when(tourBatchService.deleteBatchById(1L)).thenReturn(true);
		mockMvc.perform(MockMvcRequestBuilders.delete("/batches/1").contentType(MediaType.APPLICATION_JSON))
				.andExpect(status().isOk());

	}

	@Test
	@DisplayName("Test for deleting tour batch for Invalid Id")
	public void deleteTourBatchTestForInvalidId() throws Exception {
		Mockito.when(tourBatchService.deleteBatchById(1L)).thenReturn(false);
		mockMvc.perform(MockMvcRequestBuilders.delete("/batches/1").contentType(MediaType.APPLICATION_JSON))
				.andExpect(status().isNotAcceptable());

	}
	
	@Test
	@DisplayName("Test for getting tour batch by start date")
	public void getTourBatchByStartDateTest() throws Exception {
		List <TourBatch> tbList = new ArrayList<>();
		Mockito.when(tourBatchService.getFilteredBatches(null, null)).thenReturn(tbList);
		
		String content = objectIdWriter.writeValueAsString(tbList);
		
		MockHttpServletRequestBuilder mockRequestBuilder = MockMvcRequestBuilders.get("/batches/startDate")
				.contentType(MediaType.APPLICATION_JSON).accept(MediaType.APPLICATION_JSON).content(content);
		
		 mockMvc.perform(mockRequestBuilder)
		 .andExpect(status().isOk())
		 .andExpect(jsonPath("$", hasSize(0)))
		 .andReturn().getResponse().getContentAsString();
	}
	@Test
	@DisplayName("Testing create batch")
	public void createBatchTest() throws Exception {
		
		TourBatch tbd = BatchControllerTest.getDummyDataTourBatch();
		Mockito.when(tourBatchService.addBatch(Mockito.anyLong() ,Mockito.any(TourBatch.class))).thenReturn(tbd);
		
		String content = objectIdWriter.writeValueAsString(tbd);

		MockHttpServletRequestBuilder mockRequestBuilder = MockMvcRequestBuilders.post("/batches/tours/1")
				.contentType(MediaType.APPLICATION_JSON)
				.accept(MediaType.APPLICATION_JSON)
				.content(content);

		mockMvc.perform(mockRequestBuilder)
		.andExpect(status().isCreated())
		.andReturn().getResponse().getContentAsString();
	}
	@Test
	@DisplayName("Testing create batch for Empty Batch")
	public void createBatchTestForEmptyBatch() throws Exception {
		
		TourBatch tbd = BatchControllerTest.getDummyDataTourBatch();
		Mockito.when(tourBatchService.addBatch(Mockito.anyLong() ,Mockito.any(TourBatch.class))).thenReturn(null);
		
		String content = objectIdWriter.writeValueAsString(tbd);

		MockHttpServletRequestBuilder mockRequestBuilder = MockMvcRequestBuilders.post("/batches/tours/1")
				.contentType(MediaType.APPLICATION_JSON)
				.accept(MediaType.APPLICATION_JSON)
				.content(content);

		mockMvc.perform(mockRequestBuilder)
		.andExpect(status().isNotFound())
		.andReturn().getResponse().getContentAsString();
	}
	
}

```
```java title="BookingControllerTest.java"
package com.jt.controller;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.status;
import java.util.Arrays;
import java.util.Date;
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Disabled;
import org.junit.jupiter.api.DisplayName;
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.extension.ExtendWith;
import org.mockito.InjectMocks;
import org.mockito.Mock;
import org.mockito.Mockito;
import org.mockito.junit.jupiter.MockitoExtension;
import org.springframework.http.MediaType;
import org.springframework.test.web.servlet.MockMvc;
import org.springframework.test.web.servlet.request.MockMvcRequestBuilders;
import org.springframework.test.web.servlet.setup.MockMvcBuilders;
import com.fasterxml.jackson.databind.ObjectMapper;
import com.fasterxml.jackson.databind.ObjectWriter;
import com.jt.model.batch.Booking;
import com.jt.model.user.MobileNumber;
import com.jt.model.user.Name;
import com.jt.model.user.Traveller;
import com.jt.service.BatchService;
import com.jt.service.BookingService;

@ExtendWith(MockitoExtension.class)
@DisplayName("TourController Testing")
public class BookingControllerTest {

	private MockMvc mockMvc;

	ObjectMapper objectMapper = new ObjectMapper();
	ObjectWriter objectIdWriter = objectMapper.writer();

	@Mock
	private BookingService bookingService;
	
	@Mock
	private BatchService batchService;
	
	
	
	@InjectMocks
	private BookingController bookingController;
	
	
	@BeforeEach
	public void setUp() {
		this.mockMvc = MockMvcBuilders.standaloneSetup(bookingController).build();
	}
	

	public static Booking dummyBookingData() {
		Booking booking = new Booking();
		Date date = new Date();
//		Traveller traveller = new Traveller(1, new Name("harsh", "fulzele"), new MobileNumber("1234567890"));
		Traveller traveller = new Traveller();
		traveller.setBookingSequence(1);
		traveller.setMobile(new MobileNumber("9022018440"));
		traveller.setName(new Name("harsh" ,"fulzele"));
	
		booking.setId(1l);
		booking.setBatchId(1l);
		booking.setDate(date);
		booking.setAmount(12000.0);
		booking.setUsername("harsh@gmail.com");
		booking.setTravellers(Arrays.asList(traveller));
		return booking;
	}

	
	@Disabled
	@Test
	@DisplayName("Testing get Bookings")
	public void getBookings() throws Exception {
		
		Mockito.when(bookingService.getAllBookings()).thenReturn(Arrays.asList(dummyBookingData()));
		
		mockMvc.perform(MockMvcRequestBuilders
		.get("/bookings")
		.contentType(MediaType.APPLICATION_JSON))
		.andExpect(status().isOk());

	}
	@Disabled
	@Test
	@DisplayName("Testing get Bookings not not found status code")
	public void getBookingsNotFound() throws Exception {
		
		Mockito.when(bookingService.getAllBookings()).thenReturn(null);
		
		mockMvc.perform(MockMvcRequestBuilders
		.get("/bookings")
		.contentType(MediaType.APPLICATION_JSON))
		.andExpect(status().isNotFound());

	}
}

```
```java title="MetadataControllerTest.java"
package com.jt.controller;

import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.status;

import java.io.UnsupportedEncodingException;
import java.util.ArrayList;
import java.util.List;
import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.DisplayName;
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.extension.ExtendWith;
import org.mockito.InjectMocks;
import org.mockito.Mock;
import org.mockito.Mockito;
import org.mockito.junit.jupiter.MockitoExtension;
import org.springframework.http.MediaType;
import org.springframework.test.web.servlet.MockMvc;
import org.springframework.test.web.servlet.request.MockMvcRequestBuilders;
import org.springframework.test.web.servlet.setup.MockMvcBuilders;

import com.fasterxml.jackson.databind.ObjectMapper;
import com.fasterxml.jackson.databind.ObjectWriter;
import com.jt.model.DisplayPair;
import com.jt.service.MetadataService;

@ExtendWith(MockitoExtension.class)
@DisplayName("TourController Testing")
public class MetadataControllerTest {

	
	private MockMvc mockMvc;
	

	@Mock
	private MetadataService metadataService;
	
	@InjectMocks
	private MetadataController metadataController;
	
	ObjectMapper objectMapper = new ObjectMapper();
	ObjectWriter objectIdWriter = objectMapper.writer();

	public static DisplayPair<String, String> getDummyDisplaiPair() {
		DisplayPair<String, String> data = new DisplayPair<>();
		data.setOptionValue("ADMIN");
		data.setOptionDisplayString("Admin");
		return data;
	}
	@BeforeEach
	public void setUp() {
		this.mockMvc = MockMvcBuilders.standaloneSetup(metadataController).build();
	}
	
	@Test
	@DisplayName("Testing metadata difficulty")
	public void getDifficultyLevel() throws UnsupportedEncodingException, Exception {
		List<DisplayPair<String, String>>difficultyLevels = new ArrayList<>();
		difficultyLevels.add(this.getDummyDisplaiPair());
		
		Mockito.when(metadataService.allDifficultyLevels()).thenReturn(difficultyLevels);
		
		mockMvc.perform(MockMvcRequestBuilders
				.get("/metadata/difficulties")
				.contentType(MediaType.APPLICATION_JSON))
				.andExpect(status().isOk());
	}
	@Test
	@DisplayName("Testing metadata difficulty")
	public void getDifficultyLevelForNotFound() throws UnsupportedEncodingException, Exception {
		List<DisplayPair<String, String>>difficultyLevels = new ArrayList<>();
		difficultyLevels.add(this.getDummyDisplaiPair());
		
		Mockito.when(metadataService.allDifficultyLevels()).thenReturn(null);
		
		mockMvc.perform(MockMvcRequestBuilders
				.get("/metadata/difficulties")
				.contentType(MediaType.APPLICATION_JSON))
				.andExpect(status().isNotFound());
	}
	@Test
	@DisplayName("Testing metadata modes")
	public void getDifficultyLevelMode() throws UnsupportedEncodingException, Exception {
		List<DisplayPair<String, String>>modesList = new ArrayList<>();
		modesList.add(this.getDummyDisplaiPair());
		
		Mockito.when(metadataService.allModes()).thenReturn(modesList);
		
		mockMvc.perform(MockMvcRequestBuilders
				.get("/metadata/modes")
				.contentType(MediaType.APPLICATION_JSON))
				.andExpect(status().isOk());
	}
	
	@Test
	@DisplayName("Testing metadata modes")
	public void getDifficultyLevelModeForInvalid() throws UnsupportedEncodingException, Exception {
		List<DisplayPair<String, String>>modesList = new ArrayList<>();
		modesList.add(this.getDummyDisplaiPair());
		
		Mockito.when(metadataService.allModes()).thenReturn(null);
		
		mockMvc.perform(MockMvcRequestBuilders
				.get("/metadata/modes")
				.contentType(MediaType.APPLICATION_JSON))
				.andExpect(status().isNotFound());
	}
	
	@Test
	@DisplayName("Testing metadata modes")
	public void getRoomTypes() throws UnsupportedEncodingException, Exception {
		List<DisplayPair<String, String>>roomType = new ArrayList<>();
		roomType.add(this.getDummyDisplaiPair());
		
		Mockito.when(metadataService.allRoomTypes()).thenReturn(roomType);
		
		mockMvc.perform(MockMvcRequestBuilders
				.get("/metadata/roomtypes")
				.contentType(MediaType.APPLICATION_JSON))
				.andExpect(status().isOk());
	}
	@Test
	@DisplayName("Testing metadata modes")
	public void getRoomTypesForNotFound() throws UnsupportedEncodingException, Exception {
		List<DisplayPair<String, String>>roomType = new ArrayList<>();
		roomType.add(this.getDummyDisplaiPair());
		
		Mockito.when(metadataService.allRoomTypes()).thenReturn(null);
		
		mockMvc.perform(MockMvcRequestBuilders
				.get("/metadata/roomtypes")
				.contentType(MediaType.APPLICATION_JSON))
				.andExpect(status().isNotFound());
	}
	@Test
	@DisplayName("Testing metadata modes")
	public void getRoles() throws UnsupportedEncodingException, Exception {
		List<DisplayPair<String, String>>rolesList = new ArrayList<>();
		rolesList.add(this.getDummyDisplaiPair());
		
		Mockito.when(metadataService.allRoles()).thenReturn(rolesList);
		
		mockMvc.perform(MockMvcRequestBuilders
				.get("/metadata/roles")
				.contentType(MediaType.APPLICATION_JSON))
				.andExpect(status().isOk());
	}
	@Test
	@DisplayName("Testing metadata modes")
	public void getRolesForInvalid() throws UnsupportedEncodingException, Exception {
		List<DisplayPair<String, String>>rolesList = new ArrayList<>();
		rolesList.add(this.getDummyDisplaiPair());
		
		Mockito.when(metadataService.allRoles()).thenReturn(null);
		
		mockMvc.perform(MockMvcRequestBuilders
				.get("/metadata/roles")
				.contentType(MediaType.APPLICATION_JSON))
				.andExpect(status().isNotFound());
	}
	
	@Test
	@DisplayName("Testing metadata modes")
	public void getBatchStatus() throws UnsupportedEncodingException, Exception {
		List<DisplayPair<String, String>>batchStatus = new ArrayList<>();
		batchStatus.add(this.getDummyDisplaiPair());
		
		Mockito.when(metadataService.allStatus()).thenReturn(batchStatus);
		
		mockMvc.perform(MockMvcRequestBuilders
				.get("/metadata/batchstatuses")
				.contentType(MediaType.APPLICATION_JSON))
				.andExpect(status().isOk());
	}
	
	@Test
	@DisplayName("Testing metadata modes")
	public void getBatchStatusForInvalid() throws UnsupportedEncodingException, Exception {
		List<DisplayPair<String, String>>batchStatus = new ArrayList<>();
		batchStatus.add(this.getDummyDisplaiPair());
		
		Mockito.when(metadataService.allStatus()).thenReturn(null);
		
		mockMvc.perform(MockMvcRequestBuilders
				.get("/metadata/batchstatuses")
				.contentType(MediaType.APPLICATION_JSON))
				.andExpect(status().isNotFound());
	}
	
}

```
```java title="TourControllerTest.java"
package com.jt.controller;

import static org.hamcrest.CoreMatchers.is;
import static org.hamcrest.Matchers.hasSize;
import static org.hamcrest.Matchers.notNullValue;
import static org.junit.jupiter.api.Assertions.assertEquals;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.jsonPath;
import static org.springframework.test.web.servlet.result.MockMvcResultMatchers.status;

import java.time.LocalDate;
import java.util.ArrayList;
import java.util.Collections;
import java.util.List;

import org.junit.jupiter.api.BeforeEach;
import org.junit.jupiter.api.Disabled;
import org.junit.jupiter.api.DisplayName;
import org.junit.jupiter.api.Test;
import org.junit.jupiter.api.extension.ExtendWith;
import org.mockito.InjectMocks;
import org.mockito.Mock;
import org.mockito.Mockito;
import org.mockito.junit.jupiter.MockitoExtension;
import org.springframework.http.MediaType;
import org.springframework.test.web.servlet.MockMvc;
import org.springframework.test.web.servlet.request.MockHttpServletRequestBuilder;
import org.springframework.test.web.servlet.request.MockMvcRequestBuilders;
import org.springframework.test.web.servlet.setup.MockMvcBuilders;

import com.fasterxml.jackson.databind.ObjectMapper;
import com.fasterxml.jackson.databind.ObjectWriter;
import com.jt.model.batch.TourBatch;
import com.jt.model.tour.Accomodation;
import com.jt.model.tour.DayPlan;
import com.jt.model.tour.DifficultyLevel;
import com.jt.model.tour.GuidedTour;
import com.jt.model.tour.Itinerary;
import com.jt.model.tour.Mode;
import com.jt.model.tour.RoomType;
import com.jt.service.BatchService;
import com.jt.service.TourService;

@ExtendWith(MockitoExtension.class)
@DisplayName("TourController Testing")
public class TourControllerTest {
	
	private MockMvc mockMvc;
	
	ObjectMapper objectMapper = new ObjectMapper();
	ObjectWriter objectIdWriter = objectMapper.writer();
	
	@Mock
	private TourService tourService;
	
	@Mock
	private BatchService batchService;
	
	@InjectMocks 
	private TourController tourController;
	
	public static GuidedTour dummyDataForTour() {
		Accomodation accomodation = new Accomodation("harsh hotel" , "nagpur" , RoomType.TWIN_BED);
		DayPlan dayPlan = new DayPlan(1 , "nagpur" , 100.0 ,"harsh", accomodation);	
		List<DayPlan> listOfDayPlan = new ArrayList<>();
		listOfDayPlan.add(dayPlan);
		Itinerary itinerary = new Itinerary(listOfDayPlan);
		
		GuidedTour guidedTour = new GuidedTour();
		guidedTour.setId(1L);
		guidedTour.setName("mumbai-leh");
		guidedTour.setStartAt("mumbai");
		guidedTour.setEndAt("leh");
		guidedTour.setDays(5);
		guidedTour.setMode(Mode.WALK.toString());
		guidedTour.setDifficultyLevel(DifficultyLevel.EASY.toString());
		guidedTour.setItinerary(itinerary);
		return guidedTour;
	}
	public static TourBatch dummyDataForBatch() {
		TourBatch tourBatch = new TourBatch();
		LocalDate start_at = LocalDate.now();
		
		tourBatch.setId(1l);
		tourBatch.setStartDate(start_at);
		tourBatch.setCapacity(100);
		tourBatch.setTour(dummyDataForTour());

		return tourBatch;
	}
	@BeforeEach
	public void setUp() {
		this.mockMvc = MockMvcBuilders.standaloneSetup(tourController).build();
	}
	
	@Test
	@DisplayName("Testing Get all tours list")
	public void getAllToursTest() throws Exception {
		List<GuidedTour> data = new ArrayList<>();
		data.add(TourControllerTest.dummyDataForTour());
		
		Mockito.when(tourService.getTours()).thenReturn(data);

		mockMvc.perform(MockMvcRequestBuilders
				.get("/tours")
				.contentType(MediaType.APPLICATION_JSON))
				.andExpect(status().isOk())
				.andExpect(jsonPath("$" , hasSize(1)))
				.andReturn().getResponse().getContentAsString();
	}
	@Test
	@DisplayName("Testing Get all tour for Not Found Status")
	public void getAllToursTestForNotFound() throws Exception {	
		Mockito.when(tourService.getTours()).thenReturn(null);

		mockMvc.perform(MockMvcRequestBuilders
				.get("/tours")
				.contentType(MediaType.APPLICATION_JSON))
				.andExpect(status().isNotFound());
	}
	@Test
	@DisplayName("Testing Get Tour by Id")
	public void getTourByIdTest() throws Exception {
		Mockito.when(tourService.getTourById(1L)).thenReturn(TourControllerTest.dummyDataForTour());
		
		mockMvc.perform(MockMvcRequestBuilders
				.get("/tours/1")
				.contentType(MediaType.APPLICATION_JSON))
				.andExpect(status().isOk())
				.andExpect(jsonPath("$.name", is("mumbai-leh")))
				.andExpect(jsonPath("$" , notNullValue()))
				.andReturn().getResponse().getContentAsString();
	}
	//Test will because not implemented status code for not found in controllers
	@Test
	@DisplayName("Testing Get Tour by Id when Invalid id passed")
	public void getTourByIdTesForInvalidId() throws Exception {
		Mockito.when(tourService.getTourById(2L)).thenReturn(null);
		 mockMvc.perform(MockMvcRequestBuilders
				.get("/tours/2")
				.contentType(MediaType.APPLICATION_JSON))
				.andExpect(status().isNotFound())
				.andReturn().getResponse().getContentAsString();
		
	}
	
	@Test
	@DisplayName("Testing for create Tour")
	public void createTourTest() throws Exception {
		
		Mockito.when(tourService.addTour(Mockito.any(GuidedTour.class))).thenReturn(TourControllerTest.dummyDataForTour());
				
		String content = objectIdWriter.writeValueAsString(TourControllerTest.dummyDataForTour());
		
		MockHttpServletRequestBuilder mockRequestBuilder = MockMvcRequestBuilders.post("/tours")
				.contentType(MediaType.APPLICATION_JSON)
				.accept(MediaType.APPLICATION_JSON)
				.content(content);
		
		mockMvc.perform(mockRequestBuilder)
				.andExpect(status().isCreated())
				.andExpect(jsonPath("$", notNullValue()))
				.andReturn().getResponse().getContentAsString();

	}
	@Test
	@DisplayName("Testing for create Tour For Invalid tour")
	public void createTourTestForNotFound() throws Exception {
		GuidedTour guidedTour = TourControllerTest.dummyDataForTour();
		Mockito.when(tourService.addTour(Mockito.any(GuidedTour.class))).thenReturn(null);
				
		String content = objectIdWriter.writeValueAsString(guidedTour);
		
		MockHttpServletRequestBuilder mockRequestBuilder = MockMvcRequestBuilders.post("/tours")
				.contentType(MediaType.APPLICATION_JSON)
				.accept(MediaType.APPLICATION_JSON)
				.content(content);
		
		mockMvc.perform(mockRequestBuilder)
				.andExpect(status().isNotAcceptable());

	}
	
	@Test
	@DisplayName("Testing for update tour")
	public void updateTourTest() throws Exception {
		
		GuidedTour guidedTour = TourControllerTest.dummyDataForTour();
		guidedTour.setName("nagpur-goa");
		
		Mockito.when(tourService.updateTour(Mockito.any(GuidedTour.class))).thenReturn(guidedTour);
		
		String content = objectIdWriter.writeValueAsString(guidedTour);
		
		MockHttpServletRequestBuilder mockRequestBuilder = MockMvcRequestBuilders.put("/tours")
					.contentType(MediaType.APPLICATION_JSON)
					.accept(MediaType.APPLICATION_JSON)
					.content(content);
		
		String result = mockMvc.perform(mockRequestBuilder)
					.andExpect(status().isOk())
					.andExpect(jsonPath("$", notNullValue()))
					.andExpect(jsonPath("$.name", is("nagpur-goa")))
					.andReturn().getResponse().getContentAsString();
		
		System.out.println("-->"+result);
	}
	@Test
	@DisplayName("Testing for invalid tour get status not modified")
	public void updateTourTestForInvalidTour() throws Exception {
		
		GuidedTour guidedTour = TourControllerTest.dummyDataForTour();
		guidedTour.setName("nagpur-goa");
		
		Mockito.when(tourService.updateTour(Mockito.any(GuidedTour.class))).thenReturn(null);
		
		String content = objectIdWriter.writeValueAsString(guidedTour);
		
		MockHttpServletRequestBuilder mockRequestBuilder = MockMvcRequestBuilders.put("/tours")
					.contentType(MediaType.APPLICATION_JSON)
					.accept(MediaType.APPLICATION_JSON)
					.content(content);
		
			mockMvc.perform(mockRequestBuilder)
					.andExpect(status().isNotModified());
	}
	
	@Test
	@DisplayName("Testing delete tour")
	public void deleteTourTest() throws Exception {
		Mockito.when(tourService.deleteTourById(1L)).thenReturn(true);
		
		mockMvc.perform(MockMvcRequestBuilders
			.delete("/tours/1")
			.contentType(MediaType.APPLICATION_JSON))
			.andExpect(status().isOk());
		
		assertEquals(tourService.deleteTourById(1l), true);
	}
	
	@Test
	@DisplayName("Testing delete tour if fails")
	public void deleteTourNotAcceptableTest() throws Exception {
		  Mockito.when(tourService.deleteTourById(2L)).thenReturn(false); // assuming 2 is a case where deletion fails
		    mockMvc.perform(MockMvcRequestBuilders
		            .delete("/tours/2")
		            .contentType(MediaType.APPLICATION_JSON))
		            .andExpect(status().isNotAcceptable());
		    assertEquals(tourService.deleteTourById(2L), false);
	}
	
	
	@Disabled
	@Test
	@DisplayName("Testing get batch by tour id")
	public void getBatchByTourId() throws Exception {
		
		List<TourBatch> tourList = new ArrayList<>();
		tourList.add(BatchControllerTest.getDummyDataTourBatch());

		Mockito.when(tourService.getTourBatches(1l)).thenReturn(tourList);
		
		String response = mockMvc.perform(MockMvcRequestBuilders
				.get("/tours/1/batches")
				.contentType(MediaType.APPLICATION_JSON))
				.andExpect(status().isOk())
				.andReturn().getResponse().getContentAsString();
			System.out.println("response-->"+response);
	}
	@Disabled
	@Test
	@DisplayName("Testing get batch by tour id when id not found")
	public void getBatchByTourIdForNotFound() throws Exception {
		Mockito.when(tourService.getTourBatches(1L)).thenReturn(null);
		
		mockMvc.perform(MockMvcRequestBuilders
				.get("/tours/1/batches")
				.contentType(MediaType.APPLICATION_JSON))
				.andExpect(status().isNotFound());
			
	}
	
	
	
	@Test
	@DisplayName("Testing Get Most Popular Tours")
	public void getMostPopularToursTest() throws Exception {
	    List<GuidedTour> popularTours = new ArrayList<>();
	    popularTours.add(TourControllerTest.dummyDataForTour());
	 
	    Mockito.when(tourService.getMostPopularTours()).thenReturn(popularTours);
	 
	    mockMvc.perform(MockMvcRequestBuilders
	            .get("/tours/popular")
	            .contentType(MediaType.APPLICATION_JSON))
	            .andExpect(status().isOk())
	            .andExpect(jsonPath("$", hasSize(1)))
	            .andReturn().getResponse().getContentAsString();
	}


	@Test
	@DisplayName("Testing Get Most Popular Tours for Not Found Status")
	public void getMostPopularToursNotFoundTest() throws Exception {	
		Mockito.when(tourService.getMostPopularTours()).thenReturn(null);

		mockMvc.perform(MockMvcRequestBuilders
				.get("/tours/popular")
				.contentType(MediaType.APPLICATION_JSON))
				.andExpect(status().isNotFound());
	}
	
	@Test
	@DisplayName("Testing Filter Tours by Duration")
	public void filterTourByDurationTest() throws Exception {
		List<GuidedTour> tours = new ArrayList<>();
		tours.add(TourControllerTest.dummyDataForTour());
	    Mockito.when(tourService.filterTourByDuration(3, 7)).thenReturn(tours);
	    mockMvc.perform(MockMvcRequestBuilders
	            .get("/tours/day")
	            .param("minDays", "3")
	            .param("maxDays", "7")
	            .contentType(MediaType.APPLICATION_JSON))
	            .andExpect(status().isOk())
	            .andExpect(jsonPath("$", hasSize(1)));
	    Mockito.when(tourService.filterTourByDuration(8, 10)).thenReturn(Collections.emptyList());
	 
	    mockMvc.perform(MockMvcRequestBuilders
	            .get("/tours/day")
	            .param("minDays", "8")
	            .param("maxDays", "10")
	            .contentType(MediaType.APPLICATION_JSON))
	            .andExpect(status().isNotFound());
	}
	
	@Test
	@DisplayName("Testing Filter Tours by Place")
	public void filteredToursByPlaceTest() throws Exception {
		List<GuidedTour> tours = new ArrayList<>();
		tours.add(TourControllerTest.dummyDataForTour());
	    Mockito.when(tourService.filteredToursByPlace("Mumbai", "Goa")).thenReturn(tours);
	 
	    mockMvc.perform(MockMvcRequestBuilders
	            .get("/tours/place")
	            .param("source", "Mumbai")
	            .param("destination", "Goa")
	            .contentType(MediaType.APPLICATION_JSON))
	            .andExpect(status().isOk())
	            .andExpect(jsonPath("$", hasSize(1)));
	    
	    Mockito.when(tourService.filteredToursByPlace("Delhi", "Jaipur")).thenReturn(Collections.emptyList());
	    mockMvc.perform(MockMvcRequestBuilders
	            .get("/tours/place")
	            .param("source", "Delhi")
	            .param("destination", "Jaipur")
	            .contentType(MediaType.APPLICATION_JSON))
	            .andExpect(status().isNotFound());
	}
	 
	@Test
	@DisplayName("Testing Filter Tours by Mode")
	public void filteredToursByModeTest() throws Exception {
		List<GuidedTour> tours = new ArrayList<>();
		tours.add(TourControllerTest.dummyDataForTour());
	    Mockito.when(tourService.filteredToursByMode(Mode.fromString("WALK"))).thenReturn(tours);
	 
	    mockMvc.perform(MockMvcRequestBuilders
	            .get("/tours/mode")
	            .param("mode", "WALK")
	            .contentType(MediaType.APPLICATION_JSON))
	            .andExpect(status().isOk())
	            .andExpect(jsonPath("$", hasSize(1)));

	    Mockito.when(tourService.filteredToursByMode(Mode.fromString("BICYCLE"))).thenReturn(Collections.emptyList());
	 
	    mockMvc.perform(MockMvcRequestBuilders
	            .get("/tours/mode")
	            .param("mode", "BICYCLE")
	            .contentType(MediaType.APPLICATION_JSON))
	            .andExpect(status().isNotFound());
	}
	 
	@Test
	@DisplayName("Testing Filter Tours by Difficulty Level")
	public void filteredToursByDifficultyLevelTest() throws Exception {
		List<GuidedTour> tours = new ArrayList<>();
		tours.add(TourControllerTest.dummyDataForTour());
	    Mockito.when(tourService.filteredToursByDifficultyLevel(DifficultyLevel.fromString("EASY"))).thenReturn(tours);
	 
	    mockMvc.perform(MockMvcRequestBuilders
	            .get("/tours/difficultyLevel")
	            .param("difficultyLevel", "EASY")
	            .contentType(MediaType.APPLICATION_JSON))
	            .andExpect(status().isOk())
	            .andExpect(jsonPath("$", hasSize(1)));

	    Mockito.when(tourService.filteredToursByDifficultyLevel(DifficultyLevel.fromString("HIGH"))).thenReturn(Collections.emptyList());
	 
	    mockMvc.perform(MockMvcRequestBuilders
	            .get("/tours/difficultyLevel")
	            .param("difficultyLevel", "HIGH")
	            .contentType(MediaType.APPLICATION_JSON))
	            .andExpect(status().isNotFound());
	}
}

```
