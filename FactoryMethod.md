Factory Method
==============

```java
package com.shjung.test.framework;

public abstract class Factory {

	public final Product create(String owner) {
		Product p = createProduct(owner);
		registerProduct(p);
		return p;
	} 
	
	protected abstract Product createProduct(String owner);
	protected abstract void registerProduct(Product p);
}

public abstract class Product {
	public abstract void use();
}
```

```java
package com.shjung.test.idcard;

import com.shjung.test.framework.Product;

public class IDCard extends Product {
	private String owner;
	
	public IDCard(String owner) {
		// TODO Auto-generated constructor stub
		this.owner = owner;
	}
	
	public void use() {
		System.out.println(owner + " of cards");
	}
	
	public String getOwner() {
		return owner;
	}
}

public class IDCardFactory extends Factory {
	
	private List<String> owners = new ArrayList<String>();

	@Override
	protected Product createProduct(String owner) {
		// TODO Auto-generated method stub
		return new IDCard(owner);
	}

	@Override
	protected void registerProduct(Product p) {
		// TODO Auto-generated method stub
		owners.add(((IDCard)p).getOwner());
	}
	
	public List<String> getOwners() {
		return owners;
	}
}
```

```java
package com.shjung.test;

import com.shjung.test.framework.Factory;
import com.shjung.test.framework.Product;
import com.shjung.test.idcard.IDCardFactory;

public class Main {

	public static void main(String[] args) {
		// TODO Auto-generated method stub
		Factory f = new IDCardFactory();
		Product p1 = f.create("a");
		Product p2 = f.create("b");
		Product p3 = f.create("c");
		
		p1.use();
		p2.use();
		p3.use();
	}
}
```