<template>
  <div>
      <!-- panggil komponenya disini -->
      <navBar :logo-home='logoHome' > </navBar>
      <formImage ></formImage>
      <pic :pic="pic"></pic>
      <footerItem> </footerItem>
  </div>
</template>

<script>
// bagian ini berisi component mana saja yang ingin kita pakai
import navBar from './components/navBar'; 
import srcLogo from '../assets/logo.png';
import formImage from './components/formImage';
import pic from './components/pic';
import formRegister from './components/formRegister'
import footerItem from './components/footerItem'
export default {
  data() {
    return {
      // data yang ada di sini akan dipakai oleh setiap komponen
      logoHome : srcLogo,
      pic: "data:image/png;base64,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",
    };
  },
  components : {
    // setelah di import harus di daftarin di komponent
    navBar,
    formImage,
    pic,
    formRegister,
    footerItem
  }
};
</script>

<style scoped>
</style>