const contractABI = [...];
const contractAddress = '0x...';

const productAuthContract = new web3.eth.Contract(contractABI, contractAddress);

async function registerProduct(name, manufacturer, batchNumber, account) {
    const result = await productAuthContract.methods
        .registerProduct(name, manufacturer, batchNumber)
        .send({ from: account });

    console.log('Product registered with ID:', result.events.ProductRegistered.returnValues.productId);
}

async function verifyProduct(productId) {
    const isAuthentic = await productAuthContract.methods
        .verifyProduct(productId)
        .call();

    console.log('Product Authenticity:', isAuthentic);
}

async function getProductDetails(productId) {
    const details = await productAuthContract.methods
        .getProductDetails(productId)
        .call();

    console.log('Product Details:', details);
}
