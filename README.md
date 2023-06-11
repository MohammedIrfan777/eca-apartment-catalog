# ECA APARTMENT CATALOG 

This Application created to register apartment, to list the all apartments or single apartment by aprtment id.  

## Steps to Setup

**1. Clone the repository** 

```bash
git clone https://github.com/MohammedIrfan777/eca.git
```

**2. Run the app using maven**

```bash
cd eca
cd eca-apartment-catalog
mvn spring-boot:run
```

That's it! The application can be accessed at `http://localhost:6092`.

You may also package the application in the form of a jar and then run the jar file like so -

```bash
mvn clean package
java -jar target/eca-apartment-catalog*.jar
```

# OR

Simply run the docker image container using docker

```bash
docker build -t ecaapartmentcatalog:latest .
docker run -d -p 6092:6092 ecaapartmentcatalog:latest
```

