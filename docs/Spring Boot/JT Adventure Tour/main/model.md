# Model
## Auth
```java title="Role.java"
package com.jt.model.auth;

import java.util.ArrayList;
import java.util.List;

import com.jt.model.DisplayPair;

public enum Role {

	ADMIN("ADMIN"), CUSTOMER("CUSTOMER");
	private final String role;
	private static List<DisplayPair<String, String>> DisplayPairList = new ArrayList<DisplayPair<String, String>>();

	public static List<DisplayPair<String, String>> getDisplayPairs() {
		for (Role s : Role.values()) {
			DisplayPairList.add(new DisplayPair<String, String>(s.name(), s.role));
		}
		return DisplayPairList;
	}

	private Role(String role) {
		this.role = role;
	}

	private Role() {
		this.role = "";
	}

	public String getRole() {
		return role;
	}

	public static Role fromString(String role) {

		try {
			return Role.valueOf(role.toUpperCase());
		} catch (IllegalArgumentException e) {
			throw new IllegalArgumentException("No enum constant for " + role);
		}
	}

	@Override
	public String toString() {
		return this.getRole();
	}

}


```
```java title="User.java"
package com.jt.model.auth;
import jakarta.persistence.Entity;
import jakarta.persistence.EnumType;
import jakarta.persistence.Enumerated;
import jakarta.persistence.Id;
import lombok.AllArgsConstructor;
import lombok.Data;
import lombok.NoArgsConstructor;

@Entity
@Data
@NoArgsConstructor
@AllArgsConstructor
public class User{
	
	private String password ;
	@Id
	private String userName ;
	
	@Enumerated(EnumType.STRING)
	private Role role;
	
}


```
## Batch
```java title="Booking.java"
package com.jt.model.batch;

import java.util.ArrayList;
import java.util.Date;
import java.util.List;

import com.fasterxml.jackson.annotation.JsonFormat;
import com.jt.model.user.Traveller;

import lombok.AllArgsConstructor;
import lombok.Data;
import lombok.NoArgsConstructor;
import jakarta.persistence.CollectionTable;
import jakarta.persistence.ElementCollection;
import jakarta.persistence.Entity;
import jakarta.persistence.GeneratedValue;
import jakarta.persistence.GenerationType;
import jakarta.persistence.Id;
import jakarta.persistence.JoinColumn;
import jakarta.persistence.Table;
@Entity
@Table(name="booking")
@Data
@NoArgsConstructor
@AllArgsConstructor
public class Booking {
	@Id
	@GeneratedValue(strategy= GenerationType.AUTO )
	private Long id;
	
	@JsonFormat(shape=JsonFormat.Shape.STRING, pattern="dd-MM-yyyy")
	private Date date;
	
	private double amount;
	
	private Long batchId;
	private String username;
	
	@ElementCollection
	@CollectionTable(name = "traveller", joinColumns = @JoinColumn(name="bookingId"))
	private List<Traveller> travellers= new ArrayList<Traveller>();

}


```
```java title="Status.java"
package com.jt.model.batch;

import java.util.ArrayList;
import java.util.List;

import com.jt.model.DisplayPair;

public enum Status {
	ACTIVE("Active"),
	FULL("Full"),
	IN_PROGRESS("In Progress"),
	CANCELLED("Cancelled"),
	COMPLETED("Completed");
	private final String status;

	public static List<DisplayPair<String, String>> getDisplayPairs() {
	 	List<DisplayPair<String, String>> DisplayPairList = new ArrayList<DisplayPair<String, String>>();
		for (Status status : Status.values()) {
			DisplayPairList.add(new DisplayPair<String, String>(status.name(), status.getStatus()));
		}
		return DisplayPairList;
	}
	 
	private Status(String status) {
		this.status = status;
	}

	private Status() {
		this.status="";
	}

	public String getStatus() {
		return status;
	}
	
	public static Status fromString(String status) {
	   
	    try {
	    	 return Status.valueOf(status.toUpperCase());
		}catch(IllegalArgumentException e) {
			throw new IllegalArgumentException("No enum constant for "+status);
		}
	}

	
	 
}


```
```java title="TourBatch.java"
package com.jt.model.batch;

import java.time.LocalDate;

import jakarta.persistence.Embedded;
import jakarta.persistence.Entity;
import jakarta.persistence.EnumType;
import jakarta.persistence.Enumerated;
import jakarta.persistence.GeneratedValue;
import jakarta.persistence.GenerationType;
import jakarta.persistence.Id;
import jakarta.persistence.JoinColumn;
import jakarta.persistence.ManyToOne;
import jakarta.persistence.Table;
import com.fasterxml.jackson.annotation.JsonFormat;
import com.jt.model.tour.GuidedTour;
import com.jt.model.user.Traveller;

import lombok.AllArgsConstructor;
import lombok.Data;
import lombok.NoArgsConstructor;

@Entity
@Table(name="tour_batch")
@Data
@NoArgsConstructor
@AllArgsConstructor
public class TourBatch {
	@Id
	@GeneratedValue(strategy= GenerationType.IDENTITY )
	private Long id;
	
	@JsonFormat(shape=JsonFormat.Shape.STRING, pattern="yyyy-MM-dd")
	private LocalDate startDate;
	
	private LocalDate endDate;
	
	@Enumerated(EnumType.STRING)
	private Status status;
	private int capacity;
	private Double perParticipantCost;
	private int availableSeats;

	@Embedded
	private Traveller guide;
	
	@ManyToOne(targetEntity = GuidedTour.class)
	@JoinColumn(name = "tourId")
	private GuidedTour tour;
	
	public void setEndDate(int duration) {
		this.endDate=getStartDate().plusDays(duration);	
	}
	@JsonFormat(shape=JsonFormat.Shape.STRING, pattern="yyyy-MM-dd")
	public void setEndDate(LocalDate endDate) {
		this.endDate=endDate;
		
	}
	
	public void setAvailableSeats(int bookedSeats ) {
		this.availableSeats=this.capacity-bookedSeats;
		if(this.availableSeats<=0) {
			this.status=Status.FULL;
		}
	}
	public void setStatus(String status) {
		this.status=Status.fromString(status);
	}


}

```
## Tour
```java title="Accomodation.java"
package com.jt.model.tour;

import jakarta.persistence.Embeddable;
import jakarta.persistence.EnumType;
import jakarta.persistence.Enumerated;
import lombok.AllArgsConstructor;
import lombok.Data;
import lombok.NoArgsConstructor;

@Embeddable
@Data
@NoArgsConstructor
@AllArgsConstructor
public class Accomodation {

	private String hotelName;
	private String address;
	
	@Enumerated(EnumType.STRING)
	private RoomType roomType;
	
	public void setRoomType(String roomType) {
		this.roomType = RoomType.fromString(roomType);
	}
	
	

}


```
```java title="DayPlan.java"
package com.jt.model.tour;

import jakarta.persistence.Embeddable;
import jakarta.persistence.Embedded;
import lombok.AllArgsConstructor;
import lombok.Data;
import lombok.NoArgsConstructor;

@Embeddable
@Data
@NoArgsConstructor
@AllArgsConstructor
public class DayPlan {

	private int dayCount;
	private String place;
	private double distance;
	private String activity;
	
	@Embedded
	private Accomodation accomodation;


}


```
```java title="DifficultyLevel.java"
package com.jt.model.tour;

import java.util.ArrayList;
import java.util.List;

import com.jt.model.DisplayPair;

public enum DifficultyLevel {
	HIGH("High"),
	MODERATE("Moderate"),
	EASY("Easy");
	private final String DifficultyLevelType;

	public static List<DisplayPair<String, String>> getDisplayPairs() {
		List<DisplayPair<String,String>> displayPairList = new ArrayList<>() ;
		for (DifficultyLevel difficulty : DifficultyLevel.values()) {
			displayPairList.add(new DisplayPair<String, String>(difficulty.name(), difficulty.DifficultyLevelType));
		}
		return displayPairList;
	}

	private DifficultyLevel(String difficultyLevelType) {
		this.DifficultyLevelType = difficultyLevelType;
	}

	public String getDifficultyLevelType() {
		return this.DifficultyLevelType;
	}
	
	public static DifficultyLevel fromString(String difficultyLevel) {
	    
	    try {
	    	return DifficultyLevel.valueOf(difficultyLevel.toUpperCase());
		}catch(IllegalArgumentException e) {
			throw new IllegalArgumentException("No enum constant for "+difficultyLevel);
		}
	}
	
}

```
```java title="GuidedTour.java"
package com.jt.model.tour;

import jakarta.persistence.Column;
import jakarta.persistence.Embedded;
import jakarta.persistence.Entity;
import jakarta.persistence.EnumType;
import jakarta.persistence.Enumerated;
import jakarta.persistence.GeneratedValue;
import jakarta.persistence.GenerationType;
import jakarta.persistence.Id;
import jakarta.persistence.PrePersist;
import jakarta.persistence.PreUpdate;
import jakarta.persistence.Table;
import lombok.AllArgsConstructor;
import lombok.Data;
import lombok.NoArgsConstructor;

@Entity
@Table(name = "guided_tour")
@Data
@NoArgsConstructor
@AllArgsConstructor
public class GuidedTour {
	
	@Id
	@GeneratedValue(strategy = GenerationType.IDENTITY)
	private Long id;
	
	@Column(unique = true)
	private String name;
	
	@Enumerated(EnumType.STRING)
	private Mode mode;
	
	@Enumerated(EnumType.STRING)
	private DifficultyLevel difficultyLevel;

	@Embedded
	private Itinerary itinerary;
	
	private String startAt;
	private String endAt;

	private int days;
	private int nights;


	public void setMode(String mode) {
		this.mode = Mode.fromString(mode);
	}
	public void setDifficultyLevel(String difficultyLevel) {
		this.difficultyLevel = DifficultyLevel.fromString(difficultyLevel);
	}
	
	@PreUpdate
	 @PrePersist
	 public void setDaysAndNights() {
		 days = itinerary.getDayPlans().size();
		 nights = days - 1;
	}

}


```
```java title="Itinerary.java"
package com.jt.model.tour;

import java.util.ArrayList;
import java.util.List;

import jakarta.persistence.CollectionTable;
import jakarta.persistence.ElementCollection;
import jakarta.persistence.Embeddable;
import lombok.AllArgsConstructor;
import lombok.Data;
import lombok.NoArgsConstructor;

@Embeddable
@Data
@NoArgsConstructor
@AllArgsConstructor
public class Itinerary {

	@ElementCollection
	@CollectionTable(name = "daily_plan")
	private List<DayPlan> dayPlans= new ArrayList<DayPlan>();

}


```
```java title="Mode.java"
package com.jt.model.tour;

import java.util.ArrayList;
import java.util.List;

import com.jt.model.DisplayPair;

public enum Mode {
	WALK("Walk"), BICYCLE("Bicycle"), MOTORBIKE("Motorbike");
	private final String ModeType;

	public static List<DisplayPair<String, String>> getDisplayPairs() {
		List<DisplayPair<String, String>> DisplayPairList = new ArrayList<DisplayPair<String, String>>();
		for (Mode mode : Mode.values()) {
			DisplayPairList.add(new DisplayPair<String, String>(mode.name(), mode.ModeType));
		}
		return DisplayPairList;
	}

	private Mode(String modeType) {
		this.ModeType = modeType;
	}

	public String getModeType() {
		return this.ModeType;
	}

	public static Mode fromString(String modeType) {

		try {
			return Mode.valueOf(modeType.toUpperCase());
		} catch (IllegalArgumentException e) {
			throw new IllegalArgumentException("No enum constant for " + modeType);
		}
	}

}


```
```java title="RoomType.java"
package com.jt.model.tour;

import java.util.ArrayList;
import java.util.List;

import com.jt.model.DisplayPair;

public enum RoomType {
    TWIN_BED("Twin Bed"), DOUBLE_BED("Double Bed");

	private final String roomType;

	RoomType(String roomType) {
		this.roomType = roomType;
	}

	public String getRoomType() {
		return roomType;
	}

	public static RoomType fromString(String roomType) {
		try {
			return RoomType.valueOf(roomType.toUpperCase());
		}
		catch(Exception e) {
			for (RoomType room : RoomType.values()) {
				System.out.println(room.getRoomType());
				if (room.getRoomType().toUpperCase().equals(roomType.toUpperCase()))
					return room;
			}
		}
		throw new IllegalArgumentException("No enum constant for " + roomType);
	}

	public static List<DisplayPair<String, String>> getDisplayPairs() {
		List<DisplayPair<String, String>> DisplayPairList = new ArrayList<DisplayPair<String, String>>();
		for (RoomType room : RoomType.values()) {
			DisplayPairList.add(new DisplayPair<String, String>(room.name(), room.roomType));
		}
		return DisplayPairList;
	}
}

```

## User
```java title="MobileNumber.java"
package com.jt.model.user;

import jakarta.persistence.Embeddable;
import lombok.AllArgsConstructor;
import lombok.Data;
import lombok.NoArgsConstructor;

@Embeddable
@Data
@NoArgsConstructor
@AllArgsConstructor
public class MobileNumber {

	private String number;

}

```
```java title="Name.java"
package com.jt.model.user;

import jakarta.persistence.Embeddable;
import lombok.AllArgsConstructor;
import lombok.Data;
import lombok.NoArgsConstructor;

@Embeddable
@Data
@NoArgsConstructor
@AllArgsConstructor
public class Name{

	private String first;
	private String last;
}

```
```java title="Traveller.java"
package com.jt.model.user;

import jakarta.persistence.Embeddable;
import jakarta.persistence.Embedded;
//import jakarta.persistence.GeneratedValue;
//import jakarta.persistence.GenerationType;
import lombok.AllArgsConstructor;
import lombok.Data;
import lombok.NoArgsConstructor;

@Data
@NoArgsConstructor
@AllArgsConstructor
@Embeddable
public class Traveller {

//	@GeneratedValue(strategy = GenerationType.AUTO)
	private int bookingSequence;
	@Embedded
	Name name;

	@Embedded
	MobileNumber mobile;


}

```
```java title="DisplayPair.java"
package com.jt.model;

import lombok.AllArgsConstructor;
import lombok.Data;
import lombok.NoArgsConstructor;

@Data
@NoArgsConstructor
@AllArgsConstructor
public class DisplayPair<U,V> {
	private U optionValue;
	private V optionDisplayString;
}

```
