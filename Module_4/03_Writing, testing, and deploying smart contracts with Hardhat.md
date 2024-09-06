### Escribir, Probar y Desplegar Contratos Inteligentes con Hardhat

Aquí tienes un resumen detallado de cómo escribir, probar y desplegar contratos inteligentes utilizando **Hardhat**:

#### 1. Escribir un Contrato Inteligente

Crea un archivo llamado `contracts/MyContract.sol` con el siguiente código Solidity:

```solidity
// contracts/MyContract.sol
pragma solidity ^0.8.0;

contract MyContract {
  function greet() public pure returns (string memory) {
    return "Hello, Hardhat!";
  }
}
```

Este contrato contiene una función `greet()` que simplemente devuelve el mensaje "Hello, Hardhat!".

#### 2. Probar el Contrato Inteligente

Crea un archivo de prueba en el directorio `test/` llamado `MyContract.test.js` con el siguiente código JavaScript:

```javascript
// test/MyContract.test.js
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
```

En esta prueba:
- Se utiliza **Ethers.js** para desplegar el contrato.
- Se verifica que la función `greet()` devuelve el mensaje esperado.

#### 3. Desplegar el Contrato Inteligente

Crea un archivo de despliegue en el directorio `scripts/` llamado `deploy.js` con el siguiente código JavaScript:

```javascript
// scripts/deploy.js
const { ethers } = require("hardhat");

async function main() {
  const MyContract = await ethers.getContractFactory("MyContract");
  const myContract = await MyContract.deploy();
  await myContract.deployed();
  console.log("Contract deployed to:", myContract.address);
}

main();
```

Este script:
- Obtiene la fábrica del contrato (`getContractFactory`).
- Despliega el contrato y espera a que esté desplegado (`deploy` y `deployed`).
- Imprime la dirección del contrato desplegado en la consola.

#### 4. Ejecutar la Prueba y Desplegar el Contrato

Para ejecutar las pruebas y desplegar el contrato, utiliza los siguientes comandos:

1. **Ejecutar la prueba**:

    ```bash
    npx hardhat test
    ```

    Este comando ejecutará las pruebas definidas en el archivo `MyContract.test.js` y mostrará si las pruebas pasaron o fallaron.

2. **Desplegar el contrato**:

    ```bash
    npx hardhat run scripts/deploy.js
    ```

    Este comando ejecutará el script `deploy.js` y desplegará el contrato en la red local de Hardhat.

### Resumen de los Pasos:

1. **Escribir el Contrato**: Crea el archivo Solidity con el código del contrato.
2. **Probar el Contrato**: Define pruebas utilizando **Chai** y **Ethers.js** para verificar la funcionalidad del contrato.
3. **Desplegar el Contrato**: Crea un script de despliegue para implementar el contrato en la red.
4. **Ejecutar la Prueba y Desplegar**: Utiliza los comandos de Hardhat para probar y desplegar el contrato.

Puedes ajustar la configuración y agregar características adicionales según sea necesario para tu proyecto. Si necesitas más detalles o tienes preguntas adicionales, ¡no dudes en preguntar!