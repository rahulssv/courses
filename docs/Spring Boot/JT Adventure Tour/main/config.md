# Config
```java title="SecurityConfig.java"
package com.jt.config;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.http.HttpMethod;
import org.springframework.security.authentication.AuthenticationManager;
import org.springframework.security.authentication.AuthenticationProvider;
import org.springframework.security.authentication.dao.DaoAuthenticationProvider;
import org.springframework.security.config.Customizer;
import org.springframework.security.config.annotation.authentication.configuration.AuthenticationConfiguration;
import org.springframework.security.config.annotation.method.configuration.EnableMethodSecurity;
import org.springframework.security.config.annotation.web.builders.HttpSecurity;
import org.springframework.security.config.annotation.web.configuration.EnableWebSecurity;
import org.springframework.security.config.http.SessionCreationPolicy;
import org.springframework.security.core.userdetails.UserDetailsService;
import org.springframework.security.crypto.bcrypt.BCryptPasswordEncoder;
import org.springframework.security.crypto.password.PasswordEncoder;
import org.springframework.security.web.SecurityFilterChain;
import org.springframework.security.web.authentication.UsernamePasswordAuthenticationFilter;


import com.jt.auth.JwtAuthFilter;

@Configuration
@EnableWebSecurity
@EnableMethodSecurity
public class SecurityConfig {
	@Autowired
	private JwtAuthFilter authFilter ;
	
	@Bean
	public UserDetailsService userDetailsService() {
		return new UserInfoUserDetailsService() ;
	}
	
	@Bean
	public PasswordEncoder passwordEncoder() {
		return new BCryptPasswordEncoder() ;
	}
	
	@Bean
	public SecurityFilterChain securityFilterChain(HttpSecurity http)throws Exception {
		return http.csrf().disable()
		.cors(Customizer.withDefaults())
		.authorizeHttpRequests()
		.requestMatchers(HttpMethod.GET,"/tours").permitAll()
		.requestMatchers(HttpMethod.GET,"/tours/{tourId}/batches").permitAll()
		.requestMatchers(HttpMethod.GET,"/tours/{id}").permitAll()
		.requestMatchers("/tours/day").permitAll()
		.requestMatchers(HttpMethod.GET,"/batches").permitAll()
		.requestMatchers("/batches/startDate").permitAll()
		.requestMatchers(HttpMethod.GET,"/batches/{id}").permitAll()
		.requestMatchers("/auth/login").permitAll()
		.requestMatchers("/auth/register").permitAll()
		.requestMatchers("/metadata/**").permitAll()
		.and()
		.authorizeHttpRequests().requestMatchers("/auth/**")
		.authenticated().and()
		.authorizeHttpRequests().requestMatchers("/tours/**")
		.authenticated().and()
		.authorizeHttpRequests().requestMatchers("/batches/**")
		.authenticated().and()
		.authorizeHttpRequests().requestMatchers("/bookings/**")
		.authenticated().and()
		.sessionManagement()
		.sessionCreationPolicy(SessionCreationPolicy.STATELESS)
		.and()
		.authenticationProvider(authenticationProvider())
		.addFilterBefore(authFilter, UsernamePasswordAuthenticationFilter.class).build() ;
	}
	
	@Bean
	public AuthenticationProvider authenticationProvider() {
		DaoAuthenticationProvider authenticationProvider = new DaoAuthenticationProvider() ;
		authenticationProvider.setUserDetailsService(userDetailsService());
		authenticationProvider.setPasswordEncoder(passwordEncoder());
		return authenticationProvider ;
	}
	
	@Bean
	public AuthenticationManager authenticationManager(AuthenticationConfiguration config) throws Exception {
		return config.getAuthenticationManager() ;
	}
	
}

```

```java title="UserInfoUserDetails.java"
package com.jt.config;

import java.util.Arrays;
import java.util.Collection;
import java.util.List;
import java.util.stream.Collectors;

import org.springframework.security.core.GrantedAuthority;
import org.springframework.security.core.authority.SimpleGrantedAuthority;
import org.springframework.security.core.userdetails.UserDetails;

import com.jt.model.auth.User;

public class UserInfoUserDetails implements UserDetails {
	
	private String email ;
	private String password ;
	private List<GrantedAuthority> authorities ;
	
	public UserInfoUserDetails(User user) {
		email = user.getUserName() ;
		password = user.getPassword() ;
		authorities = Arrays.stream(user.getRole().toString().split(","))
				.map(SimpleGrantedAuthority::new)
				.collect(Collectors.toList()) ;
	}
	
	@Override
	public Collection<? extends GrantedAuthority> getAuthorities() {
		return authorities;
	}
	@Override
	public String getPassword() {
		return password;
	}
	@Override
	public String getUsername() {
		return email;
	}
	@Override
	public boolean isAccountNonExpired() {
		return true;
	}
	@Override
	public boolean isAccountNonLocked() {
		return true;
	}
	@Override
	public boolean isCredentialsNonExpired() {
		return true;
	}
	@Override
	public boolean isEnabled() {
		return true;
	}
	
}

```

```java title="UserInfoUserDetailsService.java"
package com.jt.config;

import java.util.Optional;

import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.security.core.userdetails.UserDetails;
import org.springframework.security.core.userdetails.UserDetailsService;
import org.springframework.security.core.userdetails.UsernameNotFoundException;
import org.springframework.stereotype.Component;

import com.jt.model.auth.User;
import com.jt.repository.UserRepository;

@Component
public class UserInfoUserDetailsService implements UserDetailsService {
	
	@Autowired
	private UserRepository repository ;
	
	
	@Override
	public UserDetails loadUserByUsername(String username) throws UsernameNotFoundException {
	
		Optional<User> userInfo =  repository.findByUserName(username) ;
		return userInfo.map(UserInfoUserDetails::new)
		.orElseThrow(()->new UsernameNotFoundException("user not found")) ;
		
	}

}


```
