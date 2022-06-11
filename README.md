# Abstract Factory Design Pattern

Abstract Factory is a creational design pattern that lets you produce families of related objects without specifying their concrete classes.

Suppose you want to support creation of Standard and Premium hotel rooms, along with that you also want to allow creation of Standard and Premium food.

```java
public class Room {
	
}

public class StandardCityViewRoom extends Room {

}

public class StandardSeaViewRoom extends Room {

}

public class StandardKingBedCityViewRoom extends Room {

}

public class StandardKingBedSeaViewRoom extends Room {

}

public class PremiumCityViewRoom extends Room {

}

public class PremiumSeaViewRoom extends Room {

}

public class PremiumKingBedCityViewRoom extends Room {

}

public class PremiumKingBedSeaViewRoom extends Room {

}

public enum BedType {
     KING_BED, SINGLE_BED;
}

public enum View {
     SEA_VIEW, CITY_VIEW;
}

public class RoomFactory {
	
    public Room getRoom(Package packageType , BedType bedType, View view) {
	  Room room = null;
		
	  if (packageType == Package.STANDARD) {
	      if (bedType == BedType.SINGLE_BED) {
		 if (view == View.CITY_VIEW) {
		     room = new StandardCityViewRoom();
		  } else if(view == View.SEA_VIEW) {
		     room = new StandardSeaViewRoom();
		  }
	      } else if(bedType == BedType.KING_BED) {
	         if (view == View.CITY_VIEW) {
		     room = new StandardKingBedCityViewRoom();
		 } else if(view == View.SEA_VIEW) {
		     room = new StandardKingBedSeaViewRoom();
		 }
	      }
	   } else if (packageType == Package.PREMIUM) {
	       if (bedType == BedType.SINGLE_BED) {
		   if (view == View.CITY_VIEW) {
		       room = new PremiumCityViewRoom();
		   } else if(view == View.SEA_VIEW) {
		       room = new PremiumSeaViewRoom();
		   }
		} else if(bedType == BedType.KING_BED) {
		   if (view == View.CITY_VIEW) {
		       room = new PremiumKingBedCityViewRoom();
		   } else if(view == View.SEA_VIEW) {
		       room = new PremiumKingBedSeaViewRoom();
		   }
		}
	    }
	   return room;	
	}

}

public enum Meal {
     BREAKFAST, LUNCH, DINNER;
}

public class StandardBreakfast extends Food {

}
public class StandardLunch extends Food {

}
public class StandardDinner extends Food {

}
public class PremiumBreakfast extends Food {

}
public class PremiumLunch extends Food {

}
public class PremiumDinner extends Food {

}

public class FoodFactory {
	public Food getFood(Package packageType, Meal meal) {
		Food food = null;
		if (packageType == Package.STANDARD) {
			if (meal == Meal.BREAKFAST) {
				food = new StandardBreakfast();
			} else if (meal == Meal.LUNCH) {
				food = new StandardLunch();
			} else if (meal == Meal.DINNER) {
				food = new StandardDinner();
			}
		} else if(packageType == Package.PREMIUM) {
			if (meal == Meal.BREAKFAST) {
				food = new PremiumBreakfast();
			} else if (meal == Meal.LUNCH) {
				food = new PremiumLunch();
			} else if (meal == Meal.DINNER) {
				food = new PremiumDinner();
			}
		}
		return food;
	}
}

```


