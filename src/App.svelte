<script>
    import List1 from "./List1.svelte";
    import Toggle from "./Toggle.svelte";
    import Else from "./Else.svelte";
    import Each from "./Each.svelte";
    import Input from "./Input.svelte";
    import Form from "./Form.svelte";
    import Reactivity from "./Reactivity.svelte";
    import EventAndFctInline from "./EventAndFctInline.svelte";
    import ChildToParent from "./ChildToParent.svelte";
    import Modal from "./Modal.svelte";
    import Onglet from "./Onglet.svelte";
    import NavBar from "./NavBar.svelte";

    //store

    import storeData from './store/store';

    let txt;
    //permet de souscrire à un store et mettre à jour des données en cas de changements
    storeData.subscribe((value) => {
        txt = value;
    })
    //permet de modifier les valeur dans le store
    storeData.set('Lorem ipsus')

    //Mettre à  jour le store à partir des données du store
    //storeData.update(value => value + 10) ex 20 si a la base value = 10


    //custom Store
    import CustomStore from "./store/store2";

    let data;

    CustomStore.subscribe((value) => {
        data = value;
    });

    CustomStore.addBox({id: 4, text: 'Lorem4'});

    let titre = "Mes lignesssss";

    let myObject = {
        nationality: "english",
        taille: 170,
        religion: "protestant",
        married: false,
    };

    let compteur = 0;
    const increment = () => {
        compteur++;
    }

    const decrement = () => {
        compteur--;
    }

    const reset = () => {
        compteur = 0;
    }

    const fonctionParent = (event) => {
        console.log('Quelque chose a changé' + event.detail.customtxt);
    }
    let toggle = false;
    let toggleModal = false;
    const handleModal = () => {
        toggleModal = !toggleModal
    };

</script>


<main>


    <NavBar/>

    {#each data as box (box.id)}
        <div>
            <h2>{box.text}</h2>
            <h3>{box.id}</h3>
        </div>
    {/each}
    <h1>{txt}</h1>

    <div class="flex justify-around">
        <List1 class="p-1" montitre={titre} {...myObject}/>
        <div class="p-1"><p>{compteur}</p>
            <button on:click={increment}>+1</button>
            <button on:click={decrement}>-1</button>
            <button on:click={reset}>Reset</button>
        </div>
        <Toggle class="p-1"/>
        <Else class="p-1"/>
        <Each class="p-1"/>

    </div>
    <div class="flex justify-around">
        <Input/>
        <Form/>
        <Reactivity/>
    </div>
    <div class="flex justify-around">
        <EventAndFctInline/>
        <div>
            <h2>Je suis le parent !</h2>
            <button class="my-1" on:click={()=>toggle=!toggle}>Affiche le gosse</button>
            {#if toggle}
                <ChildToParent on:info-carte={fonctionParent}>
                    <h2>Mon titre depuis le parent</h2>
                    <div slot="contenu">
                        <p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. A, consequuntur corporis
                            debitis
                            eligendi
                            eum hic minus, nemo, omnis reprehenderit similique totam vero voluptas voluptatibus
                            voluptatum?</p>
                    </div>
                </ChildToParent>
            {/if}
        </div>

    </div>

    <div class="flex justify-around">
        <div>
            <button class="my-1" on:click={handleModal}>Affiche le modal</button>
            {#if toggleModal}
                <Modal on:overlayModal={handleModal}/>
            {/if}
        </div>
        <div>
            <Onglet/>
        </div>
    </div>


</main>

<style global>
    @import 'tailwindcss/base';

    @import 'tailwindcss/components';

    @import 'tailwindcss/utilities';

</style>