<script>
  import { getContext } from 'svelte';
  const { Socket } = getContext('connect');
  const socket = Socket();
  import wordDb from '../assets/db';
  const randomWords = wordDb;

  const drawer = JSON.parse(sessionStorage.getItem('drawer'));
  const socketId = sessionStorage.getItem('socketid');

  function startGame() {
    socket.emit('start', randomWords[Math.floor(Math.random() * randomWords.length)].word);
  }
</script>

<input type="checkbox" id="my-modal" class="modal-toggle" checked />
<div class="modal">
  <div class="modal-box flex flex-col items-center">
    <h3 class="font-bold text-lg text-error">Game RULES:</h3>
    <h4 class="text-success">
      When its your turn to draw, you will be assigned a word. You must visualize that word(as a
      drawing) in 50 seconds. When somebody else is drawing you have to type your guess into the
      chat to gain points, be quick, the earlier you guess a word the more points you get!
    </h4>
    <p class="py-4 text-2x text-error">
      <span class="text-secondary"> {drawer.name} </span> is the first drawer
    </p>
    {#if socketId === drawer.id}
      <div class="modal-action">
        <label for="my-modal" class="btn btn-accent" on:click={startGame}>Lets goooo!</label>
      </div>
    {/if}
  </div>
</div>
