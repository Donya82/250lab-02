# Lab 2
[Fork](https://docs.github.com/en/get-started/quickstart/fork-a-repo) this repo and clone it to your machine to get started!

## Team Members
- Donya Badamchi
- Melissa Shun

## Lab Question Answers

Question 1: How did the reliability of UDP change when you added 50% loss to your local
environment? Why did this occur?
At some point no message would get sent thgrough of the 10 would send not all woul get to the the first terminal. 

Question 2: How did the reliability of TCP change? Why did this occur?
The reliability did not change 

Question 3: How did the speed of the TCP response change? Why might this happen?
The speed at which the messages got sent was much slower. It would take multiple seconds for teh messages to get through.
...

/* A simple server in the internet domain using TCP
 * Answer the questions below in your writeup
 */
#include <stdio.h>
#include <stdlib.h>
#include <string.h>
#include <unistd.h>
#include <sys/types.h> 
#include <sys/socket.h>
#include <netinet/in.h>

void error(const char *msg)
{
    perror(msg);
    exit(1);
}

int main(int argc, char *argv[])
{
    /* 1. What is argc and *argv[]?
     * argc is the number of arguments on the command line while argv[] is an array containing the string of argument 
     */
    int sockfd, newsockfd, portno;
    /* 2. What is a UNIX file descriptor and file descriptor table?
     * the Unix file descriptor is an integer value that identifies a file. The file descriptor file is a collection of interger array indices that 
     */
    socklen_t clilen;

    struct sockaddr_in serv_addr, cli_addr;
    /* 3. What is a struct? What's the structure of sockaddr_in?
     * struct is a way to put together multiple related variables. sockaddr_in specifies a transport address and port for the AF_INET address family
     */
    
    int n;
    if (argc < 2) {
        fprintf(stderr,"ERROR, no port provided\n");
        exit(1);
    }
    
    sockfd = socket(AF_INET, SOCK_STREAM, 0);
    /* 4. What are the input parameters and return value of socket()
     * the input parameters are int domain, int type, int protocol. The return value of socket is the file descriptor for the new socket
     */
    
    if (sockfd < 0) 
       error("ERROR opening socket");
    bzero((char *) &serv_addr, sizeof(serv_addr));
    portno = atoi(argv[1]);
    serv_addr.sin_family = AF_INET;
    serv_addr.sin_addr.s_addr = INADDR_ANY;
    serv_addr.sin_port = htons(portno);
    
    if (bind(sockfd, (struct sockaddr *) &serv_addr,
             sizeof(serv_addr)) < 0) 
             error("ERROR on binding");
    /* 5. What are the input parameters of bind() and listen()?
     *input parameters of bind() are int sockfd, const struct sockaddr *addr, socklen_t addrlen
     input parameters of bind() are int sockfd, int backlog
     */
    
    listen(sockfd,5);
    clilen = sizeof(cli_addr);
    
    while(1) {
        /* 6.  Why use while(1)? Based on the code below, what problems might occur if there are multiple simultaneous connections to handle?
        *
        */
        
	char buffer[256];
        newsockfd = accept(sockfd, 
                    (struct sockaddr *) &cli_addr, 
                    &clilen);
	/* 7. Research how the command fork() works. How can it be applied here to better handle multiple connections?
         * The fork() command works by creating a branch that creates a new process which then allows both branches to run the next instruction followed by the fork() call. This allows a user to run commands on multiple connectioin at the same time instead of having to do them all separatly.
         */
        
	if (newsockfd < 0) 
             error("ERROR on accept");
	bzero(buffer,256);
        
	n = read(newsockfd,buffer,255);
        if (n < 0) 
            error("ERROR reading from socket");
        printf("Here is the message: %s\n",buffer);
        n = write(newsockfd,"I got your message",18);
        if (n < 0) 
            error("ERROR writing to socket");
        close(newsockfd);
    }
    close(sockfd);
    return 0; 
}
  
/* This program makes several system calls such as 'bind', and 'listen.' What exactly is a system call?
 * a way that a program can inact a service from the operating system
 */
