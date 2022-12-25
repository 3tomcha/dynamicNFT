<script setup lang="ts">
import { ethers } from "ethers";
import MyNFTAbi from "@/abi/MyNFT.json";
import type { MyNFT } from "@/typechain-types/contracts/index";
const contractAddress = "0x3AC57EdafED16c97bAc03c2911E609D63dc1148e";

const load = async () => {
  const provider = new ethers.providers.Web3Provider((window as any).ethereum);
  await provider.send("eth_requestAccounts", []);
  const signer = await provider.getSigner();
  console.log(signer)
  const myNFT = (await new ethers.Contract(contractAddress, MyNFTAbi.abi, signer)) as MyNFT;
  console.log(myNFT)
  console.log(await myNFT.name());
}
</script>

<template>
  <div class="about" @click="load">
    <h1>This is an about page</h1>
  </div>
</template>

<style>
@media (min-width: 1024px) {
  .about {
    min-height: 100vh;
    display: flex;
    align-items: center;
  }
}
</style>
