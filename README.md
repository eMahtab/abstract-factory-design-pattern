# Abstract Factory Design Pattern

Abstract Factory is a creational design pattern that lets you produce families of related objects without specifying their concrete classes.

Suppose you want to support creation of Standard and Premium hotel rooms, along with that you also want to allow creation of Standard and Premium food.

```java
public enum Package {
	STANDARD, PREMIUM;
}

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

public class Main {
    public static void main(String[] args) {
	RoomFactory roomFactory = new RoomFactory();
	FoodFactory foodFactory = new FoodFactory();
		
	Room room = roomFactory.getRoom(Package.STANDARD, BedType.SINGLE_BED, View.SEA_VIEW);
	Food food = foodFactory.getFood(Package.PREMIUM, Meal.LUNCH);	
    }
}

```

The problem with the above implementation is we want to restrict packaging the Premium food types with the Standard Room types.
But above implementation allows combining the Standard room types with Premium food types.

### AbstractFactory pattern in the use

```java
public abstract class PackageFactory {
      public abstract Room getRoom(BedType bedType, View view);
      public abstract Food getFood(Meal meal);
	
      public static PackageFactory getFactory(Package packageType) {
	  PackageFactory packageFactory = null;
	  switch(packageType) {
            case STANDARD : packageFactory = new StandardPackage();
	    case PREMIUM : packageFactory = new PremiumPackage();
	    default : try {
			throw new Exception("No factory for " + packageType);
		      } catch (Exception e) {
			e.printStackTrace();
		      }		  
	  }
	 return packageFactory;
     } 
}


public class StandardPackage extends PackageFactory{
      
      public Room getRoom(BedType bedType, View view) {
	  Room room = null;
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
	 return room;
      }

      public Food getFood(Meal meal) {
	  Food food = null;
	  if (meal == Meal.BREAKFAST) {
	     food = new StandardBreakfast();
	  } else if (meal == Meal.LUNCH) {
	     food = new StandardLunch();
	  } else if (meal == Meal.DINNER) {
	     food = new StandardDinner();
	  }
	 return food;
      }
}


public class PremiumPackage extends PackageFactory{
    @Override
    public Room getRoom(BedType bedType, View view) {
      Room room = null;
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
      return room;	
     }

     @Override
     public Food getFood(Meal meal) {
	Food food = null;
	if (meal == Meal.BREAKFAST) {
	   food = new PremiumBreakfast();
	} else if (meal == Meal.LUNCH) {
	   food = new PremiumLunch();
	} else if (meal == Meal.DINNER) {
	   food = new PremiumDinner();
	}
       return food;
     }
}


public class Main {
    public static void main(String[] args) {
	PackageFactory factory = PackageFactory.getFactory(Package.STANDARD);
		
	Room room = factory.getRoom(BedType.SINGLE_BED, View.SEA_VIEW);
	Food food = factory.getFood(Meal.LUNCH);		
    }
}

```

With the code implementing the Abstract Factory pattern , we have taken out the Package type from the getRoom() and getFood() method signature.
