# SpringDemo1
User.java
    package com.example.SpringBootExmp1.Entity;

import javax.persistence.Entity;
import javax.persistence.GeneratedValue;
import javax.persistence.GenerationType;
import javax.persistence.Id;

@Entity
public class User {
	@Id
	@GeneratedValue(strategy=GenerationType.AUTO)
	private int id;
	private String name;
	private String email;
	private String mobNumber;
	public int getId() {
		return id;
	}
	public void setId(int id) {
		this.id = id;
	}
	public String getName() {
		return name;
	}
	public void setName(String name) {
		this.name = name;
	}
	public String getEmail() {
		return email;
	}
	public void setEmail(String email) {
		this.email = email;
	}
	public String getMobNumber() {
		return mobNumber;
	}
	public void setMobNumber(String mobNumber) {
		this.mobNumber = mobNumber;
	}
	
	

}


UserRepo:-

   package com.example.SpringBootExmp1.Repository;

import org.springframework.data.jpa.repository.JpaRepository;
import org.springframework.stereotype.Repository;

import com.example.SpringBootExmp1.Entity.User;

@Repository
public interface UserRepository extends JpaRepository<User, Integer> {

}




MainController:-
   
   package com.example.SpringBootExmp1.Controller;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.http.ResponseEntity;
import org.springframework.web.bind.annotation.PostMapping;
import org.springframework.web.bind.annotation.RequestBody;
import org.springframework.web.bind.annotation.RestController;

import com.example.SpringBootExmp1.Entity.User;
import com.example.SpringBootExmp1.Service.MainService;

@RestController
public class MainController {
	
	@Autowired
	MainService mainService;
	
	@PostMapping("/save")
	public ResponseEntity<?> saveUser(@RequestBody User user){
		mainService.saveUser(user);
		return ResponseEntity.ok("User Saved Successfully");		
	}

}


MainService:-
    
    package com.example.SpringBootExmp1.Service;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Service;

import com.example.SpringBootExmp1.Entity.User;
import com.example.SpringBootExmp1.Repository.UserRepository;

@Service
public class MainService {
	
	@Autowired
	UserRepository userRepo;

	public void saveUser(User user) {
		userRepo.save(user);
		// TODO Auto-generated method stub
		
	}

}



Application Properties:-
   
   
   server.port=8080
spring.datasource.url=jdbc:mysql://localhost:3306/SpringDemo?createDatabaseIfnotExist=true&useSSL=false
spring.datasource.username=root
spring.datasource.password=root

spring.jpa.properties.hibernate.dialect=org.hibernate.dialect.MySQL5Dialect
spring.jpa.hibernate.ddl.auto=update
spring.jpa.properties.hibernate.format_sql=true









