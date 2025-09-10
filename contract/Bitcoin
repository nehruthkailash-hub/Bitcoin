// SPDX-License-Identifier: MIT
pragma solidity ^0.8.19;

/**
 * @title Bitcoin
 * @dev A simplified Bitcoin-inspired smart contract
 */
contract Project {
    string public constant name = "Bitcoin";
    string public constant symbol = "BTC";
    uint8 public constant decimals = 8;
    uint256 public constant MAX_SUPPLY = 21_000_000 * 10**decimals;

    uint256 public totalSupply;
    address public owner;

    mapping(address => uint256) public balances;
    mapping(address => bool) public authorizedMiners;

    event Transfer(address indexed from, address indexed to, uint256 value);
    event Mined(address indexed miner, uint256 reward);
    event MinerAuthorized(address indexed miner);

    modifier onlyOwner() {
        require(msg.sender == owner, "Only owner");
        _;
    }

    modifier onlyMiner() {
        require(authorizedMiners[msg.sender], "Not a miner");
        _;
    }

    constructor() {
        owner = msg.sender;
        authorizedMiners[owner] = true;
        emit MinerAuthorized(owner);
    }

    // Core Function 1: Transfer BTC
    function transfer(address _to, uint256 _amount) external returns (bool) {
        require(_to != address(0) && _amount > 0, "Invalid params");
        require(balances[msg.sender] >= _amount, "Insufficient balance");

        balances[msg.sender] -= _amount;
        balances[_to] += _amount;

        emit Transfer(msg.sender, _to, _amount);
        return true;
    }

    // Core Function 2: Mine BTC
    function mine() external onlyMiner {
        uint256 reward = 50 * 10**decimals;
        require(totalSupply + reward <= MAX_SUPPLY, "Max supply reached");

        balances[msg.sender] += reward;
        totalSupply += reward;

        emit Mined(msg.sender, reward);
    }

    // Core Function 3: Authorize Miner
    function authorizeMiner(address _miner) external onlyOwner {
        require(_miner != address(0), "Invalid address");
        authorizedMiners[_miner] = true;
        emit MinerAuthorized(_miner);
    }

    // View Function: Check Balance
    function balanceOf(address _addr) external view returns (uint256) {
        return balances[_addr];
    }
}
##contract
