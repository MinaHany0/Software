# API Documentation

![[API Testing V2-20250914162347829.webp]]
# Finding Hidden Parameters

![[API Testing V2-20250911212246192.webp]]
## Mass Assignment Vulnerability
![[API Testing V2-20250911212621234.webp]]
![[API Testing V2-20250911212807390.webp]]
![[API Testing V2-20250911213020737.webp]]

then comes the lab for the mass vulnerability testing
### Lab
![[API Testing V2-20250914152438483.webp]]
where the vulnerability is a hidden parameter when you are buying a jacket from the website 
- you are buying a jacket from a website
- the jacket costs 1337.00 dollars
- you have 0 dollars
- you notice that this is the checkout request![[API Testing V2-20250914152713302.webp]]
- you see that there is api/checkout, so you try to see what is there in the API endpoint![[API Testing V2-20250914152824514.webp]]
- you find that you can use POST on the checkout to make the order manually and put the data of the order yourself![[API Testing V2-20250914153140442.webp]] ![[API Testing V2-20250914153534476.webp]]
- you try the POST method and notice that an error comes with non sufficient funds
- if you concentrate, you will find a hidden parameter called discount
- you can change the discount parameter to 100 percent and then you will get the order for free ![[API Testing V2-20250914153651108.webp]]
- <span style="color:rgb(255, 192, 0)">Congratulations</span>

# Preventing Vulnerabilities in API
 ![[API Testing V2-20250914154045082.webp]]

# Server-Side Parameter Pollution to be continued Later