Spring Security SAML 2.0 Sample Test
====================

## References

#### Spring Boot
Spring Boot makes it easy to create Spring-powered, production-grade applications and services with absolute minimum fuss. It takes an opinionated view of the Spring platform so that new and existing users can quickly get to the bits they need.
- **Website:** [http://projects.spring.io/spring-boot/](http://projects.spring.io/spring-boot/)

#### Spring Security SAML Extension
Spring SAML Extension allows seamless inclusion of SAML 2.0 Service Provider capabilities in Spring applications. All products supporting SAML 2.0 in Identity Provider mode (e.g. ADFS 2.0, Shibboleth, OpenAM/OpenSSO, Ping Federate, Okta) can be used to connect with Spring SAML Extension.
- **Website:** [http://projects.spring.io/spring-security-saml/](http://projects.spring.io/spring-security-saml/)

---------

## Project description

This is a Web project.This project represents a sample implementation of a **SAML 2.0 Service Provider**, completely built on **Spring Framework**. In particular, it shows how to develop a web solution devised for Federated Authentication, by integrating **Spring Boot** and **Spring Security SAML**. The configuration has been completely defined using *Java annotations* (no XML).



---------

**1.**reconfig the ${project_path}/src/main/webapp/WEB-INF/securityContext.xml
1.1:IDP Metadata configuration - paths to metadata of IDPs in circle of trust is here. replace your entityId with ${here is the IDP metadata url}

    <bean id="metadata" class="org.springframework.security.saml.metadata.CachingMetadataManager">
		<constructor-arg>
			<list>
				<bean class="org.opensaml.saml2.metadata.provider.HTTPMetadataProvider">
					<constructor-arg>
						<value type="java.lang.String">${here is the IDP metadata url}</value>
					</constructor-arg>
					<constructor-arg>
						<value type="int">5000</value>
					</constructor-arg>
					<property name="parserPool" ref="parserPool"/>
				</bean>
			</list>
		</constructor-arg>
	</bean>
**1.2:**Filter automatically generates default SP metadata, replace your entityId with ${here is your entityId}

    <bean class="org.springframework.security.saml.metadata.MetadataGenerator">
		        <property name="entityId" value="${here is your entityId}"/>
		        <property name="extendedMetadata">
		            <bean class="org.springframework.security.saml.metadata.ExtendedMetadata">
		                <property name="signMetadata" value="false"/>
		                <property name="idpDiscoveryEnabled" value="true"/>
		            </bean>
		        </property>
		    </bean>
		</constructor-arg>
	</bean>	
	
	
**2.**When using the release zip compile the sample application available in the sample directory using: mvn package
You can find the compiled war archive spring-security-saml2-sample.war in directory sample/target/ (maven). 


**3.**You can start the application from the release sample directory using command: mvn tomcat7:run

**4.**After startup the Spring SAML sample application will be available at http://localhost:8080/spring-security-saml2-sample-test
Alternatively you can deploy the war archive to your application server or container.

**5.** register your metadata (http://localhost:8080/spring-security-saml2-sample-test/saml/metadata) to IDP server      


