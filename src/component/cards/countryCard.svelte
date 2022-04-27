<script>
	import { heartOutlined, heartFilled } from './../../assets/icons.js';
  

    export let country;
   
    let icon= heartOutlined;
    let fav = false;
    let togglefav = () => fav = !fav ;
    let arr = [];
    
    function handleClick(){ 
        togglefav();
        if(fav){   
            icon = heartFilled;
            let prevData = localStorage.getItem('country');
            let abd = JSON.parse(prevData);
            console.log(abd);
            arr=abd.concat(JSON.stringify(country));
            localStorage.setItem('country',JSON.stringify(arr))
        }
        
        else{
            icon = heartOutlined;
            localStorage.removeItem('country')
        }
    }
    

    
</script>

<div class="country">
    <img src={country.flags.png} alt={country.name.common} class="flags" />
    <div class="country-info">
        <span>
            {country?.name?.common}
        </span>
        <span>
            {country?.capital}
        </span>
        <span>
            {country?.population}
        </span>

    </div>
   
    <div class="fav-icon" on:click={handleClick}>
        
       {@html icon}

    </div>
</div>
<style>
    .country{
        display: flex;
        flex-direction: column;
        border:1px solid #ccc;
        border-radius: 10px;
        position: relative;

    }

    .country img  {
        border-top-left-radius: 10px ;     
        border-top-right-radius: 10px;  

    }
    .country-info
    {
        padding: 10px;
        display: grid;
        gap:10px;

    }
    .country-info
    {
       
    font-weight: 400;
    font-size: 20px;
    line-height: 25px;


    }
    .fav-icon{
        position: absolute;
        top: 105px;
        right: 15px;
        color:black;
        size: 20px;
    }

    /* svg{
        height: 20px;
        width: 20px;
    } */
</style>