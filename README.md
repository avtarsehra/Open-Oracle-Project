# Open Oracle Project


# Introduction
Open Oracle project is a public utility to inject web/API data into the Ethereum Classic Blockchain to trigger smart contracts easily, securely and cheaply.

#Highlevel Overview

A. Basic End-to-End Data Flow (Low complexity and simple to deploy):

1.	A user deploys an (end user) smart contract that (for example) pays out if Apple stock (AAPL) has an End of Day (EoD) price of X on a future Date Y

2.	The smart contract Includes a standard library that is used to send a transaction to the Open Oracle contract, where the transaction includes key parameters (for example):
Data Parameters:  Source=Yahoo_Finance, Feed=Stock_Price, Jurisdiction=US, Label=AAPL, Type=EoD, Date=Y

3.	Open Oracle contract stores the data request along with the requesting smart contract address, and a Blockchain event is registered that can be tracked on a tracking server

4.	Tracking server(s) monitor events, and on required date/time the tracking server requests required data from relevant API and sends transaction to the Open Oracle smart contract, which then relays to the relevant end user smart (Included Open Oracle library function) contract for triggering

5.	The end user smart contract than uses the received data to trigger relevant payoff

B. Web-Blockchain Decentralised Data Bridge (High complexity and complex to deploy):

1. As you can note above, there is a key point of failure at A.4. At this point there is a use of a centralized server that receives data requests and transmits required data to a decentralized system (called Bridging Server)

2. Storage of third party data on the Bridging Server is not completely necessary, and it may be optimal in terms of storage cost and in terms of Data usage terms and conditions to not to store any third party data permanently. In this case the Bridging Server only stores requests, executes these to fetch the required data on approriate dates, and transmits it to the Open Oracle smart contracts for relay to the relevant end user Smart Contract e.g. the AAPL payoff contract example in A.

3. Therefore, there needs to be an appropriate method to provide a decentralized mechanism with an incentive structure for a number of Bridging servers to track the Open Oracle smart contract data requests, fetch relevant data, and transmit the required data to the Open Oracle smart contract for relay

4. The decentralized mechanisms and incentive structure should encourage third parties to run the Bridging Server application, connect to the Open Oracle Smart Contract system on the Ethereum Classic Network and participate in fulfilling data requests honestly and transparently

5. A possible mechanism is that all servers send data to an Open Oracle Staging Smart Contract, which has to ensure that “most” of the data points are identical, e.g. if a tolerance of 99% is agreed, then at least 99% of the data feeds would need to have consensus for the data to be accepted and relayed to the end user contract, in which case the data request fee can be split between the Bridging Servers that agreed on the data

6. If there is a concensus discrepancy i.e. <99% agree on the data value, the Open Oracle Staging Contract can generates a failure event so all servers would need to recheck and retransmit the data
 
7. In this way new Bridging Servers can be deployed very easily, just by running the Open Oracle server application and participating in the Data Request Tracking and Tranmitting processes for a share of the fees, and their ETC account Address can be registered with the Open Oracle Staging Smart Contract to receive fees

8. A furter optimal (and competeive) model can be deployed, which would encourage fast fulfillment of data requests. In this form the staging contract would select the first 10 data feeds and share the fees between these Bridging Servers, to maximise on the reward. Therefore the remaining feeds are only used if any of the first 10 Bridging Server data feeds have discrepancies
