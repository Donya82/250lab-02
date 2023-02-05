# Lab 2
[Fork](https://docs.github.com/en/get-started/quickstart/fork-a-repo) this repo and clone it to your machine to get started!

## Team Members
- Donya Badamchi
- Melissa Shun

## Lab Question Answers

Question 1: How did the reliability of UDP change when you added 50% loss to your local
environment? Why did this occur?
A portion of the messages woudl not go through. Of teh 10 numbers 4 or 6 digitis would be sent while other messages would show nothing. I believe this is becasue UDP does not provide error correction.

Question 2: How did the reliability of TCP change? Why did this occur?
The reliability did not change. This is becaue TCP includes error detection and correction for messages lost, sent out of order, currupted, or etc.

Question 3: How did the speed of the TCP response change? Why might this happen?
The speed at which the messages got sent was much slower. It would take multiple seconds for the messages to get through. Due to TCP's error correction it takes time for the TCP to retransmitted lost messages.
...

/* 1. What is argc and *argv[]?
     * argc is the number of arguments on the command line while argv[] is an array containing the string of arguments. 
     */
   
/* 2. What is a UNIX file descriptor and file descriptor table?
     * the Unix file descriptor is an integer value that identifies a file. The file descriptor file is a collection of interger array indices used to          identify an open file.
       */
  
/* 3. What is a struct? What's the structure of sockaddr_in?
     * struct is a way to put together multiple related variables. sockaddr_in specifies a transport address and port for the AF_INET address family.
     */

/* 4. What are the input parameters and return value of socket()
     * the input parameters are int domain, int type, int protocol. The return value of socket is the file descriptor for the new socket.
     */
    
/* 5. What are the input parameters of bind() and listen()?
     *input parameters of bind() are int sockfd, const struct sockaddr *addr, socklen_t addrlen.
      input parameters of bind() are int sockfd, int backlog.
     */    
     
/* 6.  Why use while(1)? Based on the code below, what problems might occur if there are multiple simultaneous connections to handle?
      * while(1) is used to make an infinite loop, checking for commands ore recueved messages at all times. Some probelm that may occur using while (1)         with multiple connections are decreased speed and catches in the code (while works with line by line cose so if at anypoint there is an erorr the          rest of the code will not be excecuted)
      */

/* 7. Research how the command fork() works. How can it be applied here to better handle multiple connections?
      * The fork() command works by creating a branch that creates a new process which then allows both branches to run the next instruction followed by       the fork() call. This allows a user to run commands on multiple connectioin at the same time instead of having to do them all separatly.
      */
        
/* 8. This program makes several system calls such as 'bind', and 'listen.' What exactly is a system call?
      * A way that a program can inact a service from the operating system.
      */
