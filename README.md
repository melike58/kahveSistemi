# kahveSistemi



public class Main {

	public static void main(String[] args) {
		
		BaseCustomerManager customerManager = new NeroCustomerManager(new MernisServiceAdapter);
		Customer customer = new Customer(1,"Melike","özdoğan",2001,"12345");
		customerManager.Save(customer);
				
	}

}

public class Customer implements Entitiy{
	public int id;
	public String Firstname;
	public String LastName;
	public int DateOfBirth;
	public String NationalityId;
	
	public Customer(int id, String firstname, String lastName, int dateOfBirth, String nationalityId) {
		super();
		this.id = id;
		Firstname = firstname;
		LastName = lastName;
		DateOfBirth = dateOfBirth;
		NationalityId = nationalityId;
	}
	public int getId() {
		return id;
	}
	public void setId(int id) {
		this.id = id;
	}
	public String getFirstname() {
		return Firstname;
	}
	public void setFirstnama(String firstname) {
		Firstname = firstname;
	}
	public String getLastName() {
		return LastName;
	}
	public void setLastNAme(String lastName) {
		LastName = lastName;
	}
	public int getDateOfBirth() {
		return DateOfBirth;
	}
	public void setDateOfBirth(int dateOfBirth) {
		DateOfBirth = dateOfBirth;
	}
	public String getNationalityId() {
		return NationalityId;
	}
	public void setNationalityId(String nationalityId) {
		NationalityId = nationalityId;
	}
	

}

public interface CustomerService {
	void Save(Customer customer);

}

public abstract class BaseCustomerManager implements CustomerService {

	
	public  void Save(Customer customer) {
		System.out.println("Saved to database "+customer.Firstname);
		
	}

}


ublic class StarbucksCustomerManager extends BaseCustomerManager {
	
	private CustomerCheckServise _customerCheckServise;
	
	public StarbucksCustomerManager(CustomerCheckServise customerCheckServise)
	{
		_customerCheckServise = customerCheckServise;
	}
		
	public  void Save(Customer customer)
	{
		if(_customerCheckServise.CheckIfRealPerson(customer))
		{
			super.Save(customer);
		}
		else
		{
			
		 System.out.println("Not a valid person");
		}
		
	}

}


public class NeroCustomerManager extends BaseCustomerManager{
	
	private CustomerCheckServise _customerCheckServise;

	public NeroCustomerManager(CustomerCheckServise _customerCheckServise) {
		
		this._customerCheckServise = _customerCheckServise;
	}

	@Override
	public void Save(Customer customer) {
		if(_customerCheckServise.CheckIfRealPerson(customer)){
			
			super.Save(customer);
			
		}
		else {
			System.out.println("Not a valid person"); 
		}
	}
}

public class CustomerCheckManager implements CustomerCheckServise {
	

	public boolean CheckIfRealPerson(Customer customer) {
		return true;
		
	      
	}

}

public interface CustomerCheckServise {
	
	
	boolean CheckIfRealPerson(Customer customer);
	

}






