// SPDX-License-Identifier: MIT
pragma solidity ^0.8.20;

import "@openzeppelin/contracts/token/ERC721/ERC721.sol";
import "@openzeppelin/contracts/access/Ownable.sol";
import "@openzeppelin/contracts/utils/Counters.sol";

contract MyNFT is ERC721, Ownable {
    using Counters for Counters.Counter;
    Counters.Counter private _tokenIdCounter;

    constructor()
        ERC721("MyNFT", "MNFT")
        Ownable(msg.sender)
    {}

    function mintItem(address to, string memory tokenURI)
        public
        onlyOwner
        returns (uint256)
    {
        uint256 newItemId = _tokenIdCounter.current();
        _tokenIdCounter.increment();
        _safeMint(to, newItemId);
        _setTokenURI(newItemId, tokenURI);
        return newItemId;
    }
}
