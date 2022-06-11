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
```


