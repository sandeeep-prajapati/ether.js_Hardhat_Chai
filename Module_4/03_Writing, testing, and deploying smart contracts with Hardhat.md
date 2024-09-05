La escritura, prueba y despliegue de contratos inteligentes con Hardhat se puede realizar de la siguiente manera:

Escribir un contrato inteligente

Crear un archivo contracts/MyContract.sol con el siguiente código Solidity:


solidity
pragma solidity ^0.8.0;

contract MyContract {
  function greet() public pure returns (string memory) {
    return "Hello, Hardhat!";
  }
}


Probar el contrato inteligente

Crear un archivo test/MyContract.test.js con el siguiente código JavaScript:


const { expect } = require("chai");
const { ethers } = require("hardhat");

describe("MyContract", function () {
  it("Should return 'Hello, Hardhat!'", async function () {
    const MyContract = await ethers.getContractFactory("MyContract");
    const myContract = await MyContract.deploy();
    await myContract.deployed();
    expect(await myContract.greet()).to.equal("Hello, Hardhat!");
  });
});


Desplegar el contrato inteligente

Crear un archivo deploy.js con el siguiente código JavaScript:


const { ethers } = require("hardhat");

async function main() {
  const MyContract = await ethers.getContractFactory("MyContract");
  const myContract = await MyContract.deploy();
  await myContract.deployed();
  console.log("Contract deployed to:", myContract.address);
}

main();


Ejecutar la prueba y desplegar el contrato

Ejecutar los siguientes comandos:


npx hardhat test
npx hardhat run deploy.js


Esto escribirá, probará y desplegará el contrato inteligente en la red de prueba de Hardhat. Puedes personalizar la configuración y agregar más características según sea necesario.