# TryHackMe  

## Task 11: Day 5  

<img width="928" alt="image" src="https://github.com/user-attachments/assets/af436835-031b-45ac-96ea-1d2519444f09" />  

>**XML (eXtensible Markup Language)** is a method that uses **tags** to define the structure and meaning of 
data to transport and store data in a format that humans and machines can easily understand. eg `<html>` is a tag.  
>
> A **DTD(Document Type Definition)** is a set of rules that defines the structure of an XML document.
>
>**XXE(XML eXternal Entity)** is an attack or a security vulnaribility. It basically happens when an XML parser allows **external entities** to be included in
>the XML, which attackers can exploit to access sensitive data or execute malicious actions. For eg, any undesired behavious of a web app.

In this challenge, we were given a website whose address was `http://MACHINE_IP`, where the machine's IP was the [one](http://10.10.30.87/product.php) we were using at that time.   
<img width="959" alt="image" src="https://github.com/user-attachments/assets/e0c8a595-c10d-43f3-b507-f5fbd492e4b1" />  


On connecting and following the instructions, we see `Wish #21` written at checkout. 
On clicking on it, we see a forbidden page because the details are only accessible to admins.  
<img width="616" alt="image" src="https://github.com/user-attachments/assets/a54d8dbc-3dd4-4eb1-8abc-ee7f6bc95f9f" />  


So in order to see the wish, we make use of **Burp Suite** to exploit the requests.  
When we visit [this page](http://10.10.30.87/product.php), add to wishlist and switch on the intercept, we see the following kind of request:  
<img width="713" alt="image" src="https://github.com/user-attachments/assets/fcd3698e-0a9a-4fbe-8c6e-8ce19d2f5968" />  

`<product_id>` tag contains the ID of the product, which is **1** in this case.  
The `wishlist.php` accepts the request and parses the request using the following code:  
```
<?php
..
...
libxml_disable_entity_loader(false);
$wishlist = simplexml_load_string($xml_data, "SimpleXMLElement", LIBXML_NOENT);

...
..
echo "Item added to your wishlist successfully.";
?>
```

When a user sends specially crafted `XML` data to the application, the line `libxml_disable_entity_loader(false)` allows the XML parser to **load external entities**.  
This allows attackers to access sensitive data.  

Now we update the XML request that we got from this page to see the wishes.  
On sending the request to repeater and adding the following code,  
```
<!--?xml version="1.0" ?-->
<!DOCTYPE foo [<!ENTITY payload SYSTEM "/etc/hosts"> ]>
```
this introduces an external entity called **payload**.  
>A **payload** refers to the actual data or malicious content delivered by an attacker to exploit a system.

Also, in place of product ID, we added `&payload`.  
```
<product_id>
    &payload;
</product_id>
```  
The line `<!ENTITY payload SYSTEM "/etc/hosts">` tells the XML parser to replace the **`&payload`** reference with the **contents** of the file `/etc/hosts` on 
the server.   
When the XML is processed, instead of a normal `product_id`, the application tries to load and include the contents of the file specified in the entity `/etc/hosts`.  

On sending the request, got the following response which showed XXE vulnaribilties.  
<img width="318" alt="image" src="https://github.com/user-attachments/assets/82294827-4324-4f91-b6a8-e49d1bb187bd" />   

On replacing `/etc/hosts` with `/var/www/html/wishes/wish_1.txt`, we got the contents of **Wish #1**!  
<img width="710" alt="image" src="https://github.com/user-attachments/assets/217f3c62-d0cf-44cb-9435-ff1855c847e3" />  

Similarly, on changing the no of wishes, we get the contents of all different wishes.  

So, the **conclusion** as in how to prevent these vulnaribilities was to:
- Modify source code: disable external entity loading in the XML parser. In PHP, for example, we can prevent XXE by setting `libxml_disable_entity_loader(true)`
before processing the XML.  

- Always validate and sanitise the XML input: i.e recieved from users. For ex: For example, removing suspicious keywords like `/etc/host`, `/etc/passwd`, etc, from the 
request.  


<img width="950" alt="image" src="https://github.com/user-attachments/assets/3a777803-3f94-4d5a-b9f5-4fab630ed5e7" />  

For the first ques, **Wish #15** worked to get the flag.  
<img width="712" alt="image" src="https://github.com/user-attachments/assets/4c3ba81b-32f4-4950-9c00-cb5bf6c3406a" />  

Second one was found in this site http://10.10.30.87/CHANGELOG    
<img width="413" alt="image" src="https://github.com/user-attachments/assets/917c4026-2341-48a3-ac1a-563f9bd34151" />  






 












