During our Penetration Test, we came across a web server that contains JavaScript and APIs. We need to determine their functionality to understand how it can negatively affect our customer.

### Questions
- Try to study the HTML code of the webpage, and identify used JavaScript code within it. What is the name of the JavaScript file being used?
	- api.min.js
- Once you find the JavaScript code, try to run it to see if it does any interesting functions. Did you get something in return?
	- HTB{j4v45cr1p7_3num3r4710n_15_k3y}
- As you may have noticed, the JavaScript code is obfuscated. Try applying the skills you learned in this module to deobfuscate the code, and retrieve the 'flag' variable.
	- HTB{n3v3r_run_0bfu5c473d_c0d3!}
- Try to Analyze the deobfuscated JavaScript code, and understand its main functionality. Once you do, try to replicate what it's doing to get a secret key. What is the key?
	- 4150495f70336e5f37333537316e365f31355f66756e
- Once you have the secret key, try to decide it's encoding method, and decode it. Then send a 'POST' request to the same previous page with the decoded key as "key=DECODED_KEY". What is the flag you got?
	- HTB{r34dy_70_h4ck_my_w4y_1n_2_HTB}