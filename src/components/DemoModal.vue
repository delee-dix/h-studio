<template>
    <transition name="fade">
        <div class="modal-overlay" @click.self="closeModal">
            <transition name="slide">
                <div class="modal">
                    <div class="left">
                        <button class="close" @click="closeModal">Save</button>
                    </div>
                    <div class="right">
                        <button class="close" @click="closeModal">Cancel</button>
                    </div>
                    <h1>Modal</h1>
                    <p>HelloWorld</p>
                    <div class="button" @click="closeModal">Button 1</div>
                    <div class="button" @click="closeModal">Button 2</div>
                    <div class="button" @click="closeModal">Button 3</div>
                    <div class="button" @click="closeModal">Button 4</div>
                </div>
            </transition>
        </div>
    </transition>
</template>

<script>
export default {
    emits: ['close'],
    setup(_, { emit }) {
        const closeModal = () => {
            emit('close');
        };

        return {
            closeModal,
        };
    },
};
</script>

<style scoped>
.modal-overlay {
    position: fixed;
    top: 0;
    left: 0;
    width: 100%;
    height: 100%;
    background: rgba(0, 0, 0, 0.5);
    display: flex;
    justify-content: center;
    align-items: center;
    z-index: 1000;
}

.modal {
    background: white;
    padding: 20px;
    border-radius: 10px;
    width: 70%;
    height: 70%;
    /* display: flex; */
    flex-direction: column;
    /* text-align: center;
    justify-content: center; */
    box-shadow: 0 4px 6px rgba(0, 0, 0, 0.1);

    .left{
        display: flex;
        margin-left: 80%;
        button {
            background-color: black;
            color: white;
            padding: 20px 30px;
            border: 1px solid;
            border-radius: 5px;
        }
    }

    .right{
        display: flex;
        margin-left: 90%;
        button {
            background-color: white;
            padding: 20px 30px;
            border: 1px solid;
            border-radius: 5px;
        }
    }

    .close {
        position: absolute;
        cursor: pointer;
    }

    .button {
        width: auto 0;
        border: 1px solid;
        padding: 30px 0;
        margin: 15px 0;
    }
}
</style>