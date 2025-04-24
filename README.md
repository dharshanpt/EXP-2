# Experiment 2: Blockchain-Based Crowdfunding (Kickstarter Alternative)
## Aim:
To create a decentralized crowdfunding platform where donors contribute funds only if the campaign goal is met.

## Algorithm:
### step 1:

A project owner starts a campaign with a funding goal and deadline.
### step 2:

Contributors can send ETH to the campaign.
### step 3:

If the goal is met before the deadline, funds are released to the project owner.
### step 4:

If the goal is not met, contributors can withdraw their funds.

## Program:
#### Developed by: DHARSHAN PT
#### Register number: 212223230046
#### Date: 16/04/2025
```
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract Crowdfunding {
    struct Campaign {
        address creator;
        uint256 goal;
        uint256 deadline;
        uint256 amountRaised;
        bool goalMet;
        mapping(address => uint256) contributions;
    }

    Campaign public campaign;

    constructor(uint256 _goal, uint256 _duration) {
        campaign.creator = msg.sender;
        campaign.goal = _goal;
        campaign.deadline = block.timestamp + _duration;
    }

    function contribute() public payable {
        require(block.timestamp < campaign.deadline, "Campaign ended");
        campaign.amountRaised += msg.value;
        campaign.contributions[msg.sender] += msg.value;
    }

    function withdrawFunds() public {
        require(msg.sender == campaign.creator, "Only creator can withdraw");
        require(campaign.amountRaised >= campaign.goal, "Goal not met");
        payable(msg.sender).transfer(campaign.amountRaised);
        campaign.goalMet = true;
    }

    function refund() public {
        require(block.timestamp > campaign.deadline, "Campaign still active");
        require(campaign.amountRaised < campaign.goal, "Goal was met");
        uint256 amount = campaign.contributions[msg.sender];
        campaign.contributions[msg.sender] = 0;
        payable(msg.sender).transfer(amount);
    }
}
```
# Expected Output:
Users can contribute ETH to the campaign.


If the goal is met, the creator can withdraw funds.


If the goal is not met, contributors can claim a refund.


# Output :
Contribute Output : 
![contibute output](https://github.com/user-attachments/assets/a4dc0515-cd50-4fe2-a6bf-0921e5ce0724)

Withdraw Output : 
![withdrawl output](https://github.com/user-attachments/assets/0d1a9a35-7a92-4fef-8642-a49e7062f721)

Campaign Output :
![campaign output](https://github.com/user-attachments/assets/eaaaefa1-1212-4707-8a3c-dd2db8a04660)


# RESULT: 
   Thus, to create a decentralized crowdfunding platform where donors contribute funds only if the campaign goal is met is executed successfully.
