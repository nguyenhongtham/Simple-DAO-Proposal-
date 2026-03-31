# Simple-DAO-Proposal-
// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

contract SimpleDAO {
    struct Proposal {
        string description;
        uint256 voteCount;
        bool executed;
    }

    Proposal[] public proposals;
    mapping(address => bool) public members;

    constructor() {
        members[msg.sender] = true; // Founder
    }

    function addMember(address _member) public {
        require(members[msg.sender], "Not member");
        members[_member] = true;
    }

    function createProposal(string memory _description) public {
        proposals.push(Proposal(_description, 0, false));
    }

    function vote(uint256 _proposalId) public {
        require(members[msg.sender], "Not a member");
        proposals[_proposalId].voteCount++;
    }
}
