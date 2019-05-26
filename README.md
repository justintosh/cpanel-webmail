# Cpanel Email Hosting on Exabytes with Main Site on Digital Ocean

If you are looking to have your email service hosted on cPanel while having your main website hosted on another server in Digital Ocean, this might be the right guide for you. I have been struggling with not being able to send/receive emails with the droplet in Digital Ocean. Therefore, I got an email-ready with cPanel shared hosting from Exabytes to handle the email services. The following is what I did. Hope it will help you somehow. If you have a better idea or you see anything that I did is wrong, feel free to point it out. 

## What Do I Have?

- A domain purchased from Namecheap, e.g. `company.com`
- A droplet of the main site in Digital Ocean, e.g. `123.456.0.0`
- A cPanel shared hosting plan from Exabytes, e.g. `987.654.0.0`

## What Should be Done?

1. In your domain registrar, point your NAMESERVER to the following Digital Ocean nameserver:

  ```
  ns1.digitalocean.com
  ns2.digitalocean.com
  ns3.digitalocean.com
  ```
  
2. In your Digital Ocean account, create a Domain with the domain that you have, e.g. `company.com`.
3. Create an `A` record of your domain and point to your main site.

  ```
  | Type | Hostname    | Value                  | TTL (seconds) |
  |------|-------------|------------------------|---------------|
  | A    | company.com | directs to 123.456.0.0 | 3600          | 
  ```

4. Go to the domain at the browser to see if the domain is resolved correctly.
5. Create another `A` record of your domain and point to your cPanel hosting.

  ```
  | Type | Hostname    | Value                  | TTL (seconds) |
  |------|-------------|------------------------|---------------|
  | A    | company.com | directs to 987.654.0.0 | 3600          | 
  ```
  
6. Create an `A` record of your subdomain `mail.company.com` and point to your cPanel hosting.


  ```
  | Type | Hostname         | Value                  | TTL (seconds) |
  |------|------------------|------------------------|---------------|
  | A    | mail.company.com | directs to 987.654.0.0 | 3600          | 
  ```

7. Create an `MX` record of your domain and point to your domain.

  ```
  | Type | Hostname    | Value                          | TTL (seconds)  |
  |------|-------------|--------------------------------|----------------|
  | MX   | company.com | mail handled by front-sci.com. | 14400          | 
  ```

8. Go to your cPanel and create an **Addon Domain** for `company.com`. Now you should be able to use the email service provided in Cpanel while maintaining your main site in Digital Ocean. Register a new email account the test sending and receiving emails with the email address you created. 
