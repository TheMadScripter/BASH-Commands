- **Command**: ```grep -w ```
- **Description**: This allows you to get exact matches with the word/Regexp that you are using.
- **Use Case**: It comes in handy, especially when trying to parse through IP addresses. I often got issues when trying to look for an IP such as "100.0.0.10" but would end matching with other IPs such as ".101, .102, etc."

Code Example 1: Use it to find a exact match pattern within a file:
  ```
  grep -w "10.0.0.1" ./test.txt
  ```
  Example 2: Use it in a IF statement:
  ```
  if grep -w "10.0.0.1" ./test.txt > /dev/null 2>&1; then 
  	echo "The IP is present!"
  else 
  	echo "IP is not here!"
  fi
  ```
--------------------------------------------------------------------------------------------------------

- **Command**: ``` grep -c ```
- **Description**: This allows you to see a numeric value on how many times the pattern or word appears in your search.
- **Use Case**: I often use this to make it a variable to bounce against an IF statement. Helpful for me as a Network Engineer.

Code Example 1: Use it to find the amount of instances of something:

```
  username_count=$(grep -c "username " ./Router-01_configs.txt)
  if [[ $username_count ]] > "1" ; then
      echo "This device has more than one username configured locally on it" >> ./vulnerabilities.txt
  else
      echo "This device is compliant and has only one username configured locally on it" >> ./vulnerabilities.txt
  fi
```
--------------------------------------------------------------------------------------------------------
    
- **Command**: ``` grep (OR searching) ```
- **Description**: Using "\|" in conjunction with grep allows for a "OR" search.
- **Use Case**: I use this often as well when I am looking for a combination of interface ports from my backup configurations.

Code Example 1: 
```
grep "FastEthernet\|GigabitEthernet\|TenGigabitEthernet\|Vlan" ./Router-01_configs.txt
```  
Will find any instance of the above ports.

--------------------------------------------------------------------------------------------------------

- **Command**: ``` grep (Regexp searching) ```
- **Description**: Can help you find multiple patterns more dynamically.
- **Use Case**: Use this in conjunction with the grep "OR searching" to get more specific information.

Code Example 1: 
```
grep "FastEthernet0\/[0-9][0-9]\|GigabitEthernet[0-9]\/0\/[0-9][0-9]" ./Router-01_configs.txt
```
Will find any FastEthernet ports that start with 0 and go through 0-49. This will also find GigabitEthernet ports that starts with numbers 0-9 and go from 0-49.

--------------------------------------------------------------------------------------------------------
  
- **Command**: ``` grep (AND searching) ```
- **Description**: Using "&&" in conjunction with grep allows for a "AND" search.
- **Use Case**: I used this primarely when determining what type of port security my network devices used. There are different combinations that I had which this method solved for me.

Code Example 1:
```
if grep "$port-security" && grep "$port-security-sticky"; then
	port_sec="Traditional"
elif grep "$port-security" && ! grep "port-security-sticky"; then
	port-sec="Incomplete Traditional"
fi    
```	
--------------------------------------------------------------------------------------------------------
          
    
