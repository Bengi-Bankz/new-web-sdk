<script lang="ts">
import { onMount } from 'svelte';

let betLevels = [1, 2, 3];
let betIndex = 0;
let showMenu = false;
let showInfo = false;
let showBonus = false;
let showBet = false;
let sound = 50;

function updateBet(index: number) {
  betIndex = index;
}

function closeAllModals() {
  showInfo = false;
  showBonus = false;
  showBet = false;
}
</script>

<div class="ui-bar">
  <div class="ui-left">
    <button class="ui-btn menu-btn" on:click={() => showMenu = !showMenu}>☰</button>
    {#if showMenu}
      <div class="menu-drop">
        <button class="ui-btn info-btn" on:click={() => { showInfo = true; showMenu = false; }}>Game Info</button>
        <button class="ui-btn sound-btn">
          Sound
          <input type="range" min="0" max="100" bind:value={sound} class="sound-slider" />
        </button>
        <button class="ui-btn exit-btn" on:click={() => fetch('http://localhost:3000/exit', { method: 'POST' })}>Exit</button>
      </div>
    {/if}
    <button class="ui-btn bonus-btn" on:click={() => showBonus = true}><span class="star">★</span></button>
  </div>
  <div class="ui-center">
    <button class="ui-btn minus-btn" on:click={() => betIndex = Math.max(betIndex - 1, 0)}>-</button>
    <button class="ui-btn bet-btn" on:click={() => showBet = true}>${betLevels[betIndex]}</button>
    <button class="ui-btn plus-btn" on:click={() => betIndex = Math.min(betIndex + 1, betLevels.length - 1)}>+</button>
  </div>
  <div class="ui-right">
    <button class="ui-btn play-btn">Play</button>
  </div>
</div>

{#if showInfo}
  <div class="modal info-modal">
    <div class="modal-content">
      <h2>Game Info</h2>
      <p>Game information goes here.</p>
      <button class="ui-btn close-info" on:click={closeAllModals}>Close</button>
    </div>
  </div>
{/if}

{#if showBonus}
  <div class="modal bonus-modal">
    <div class="modal-content">
      <h2>Buy Bonus?</h2>
      <div class="bonus-price" style="margin: 10px 0; font-size: 1.1em; color: #ffd700;">
        Price: ${betLevels[betIndex] * 100}
      </div>
      <button class="ui-btn confirm-bonus" on:click={closeAllModals}>Confirm</button>
      <button class="ui-btn deny-bonus" on:click={closeAllModals}>Deny</button>
    </div>
  </div>
{/if}

{#if showBet}
  <div class="modal bet-modal">
    <div class="modal-content bet-scroll">
      <h2>Select Bet</h2>
      <div class="bet-options">
        {#each betLevels as bet, idx}
          <button class="ui-btn bet-option-btn" style:background={idx === betIndex ? '#81cfff' : ''} on:click={() => { updateBet(idx); closeAllModals(); }}>
            ${bet}
          </button>
        {/each}
      </div>
      <button class="ui-btn close-bet" on:click={closeAllModals}>Close</button>
    </div>
  </div>
{/if}

<style>
.ui-bar {
  position: absolute;
  left: 0; right: 0;
  height: 15vh;
  min-height: 100px;
  max-height: 200px;
  bottom: 0;
  display: flex;
  align-items: center;
  justify-content: space-between;
  background: rgba(0,0,0,0.9);
  border-radius: 24px 24px 0 0;
  margin: 0 auto;
  width: 100vw;
  pointer-events: auto;
}
.ui-left, .ui-center, .ui-right {
  display: flex;
  align-items: center;
  gap: 20px;
}
.ui-btn {
  margin: 0 10px;
}
.play-btn {
  margin-right: 5vh;
}
.ui-center {
  flex: 1;
  justify-content: center;
}
.ui-btn {
  background: #b3e0ff;
  color: #081720;
  border: 2px solid #fff;
  border-radius: 16px;
  padding: 16px 24px;
  font-size: 1.2rem;
  font-family: inherit;
  cursor: pointer;
  min-width: 56px;
  min-height: 48px;
  box-shadow: 0 2px 8px rgba(0,0,0,0.08);
  transition: background 0.2s;
  pointer-events: auto;
}
.minus-btn, .plus-btn {
  min-width: 36px;
  min-height: 36px;
  padding: 8px 12px;
  font-size: 1rem;
}
.ui-btn:active {
  background: #81cfff;
}
.star {
  font-size: 1.5em;
}
.menu-drop {
  position: absolute;
  left: 0;
  bottom: 100%;
  background: rgba(0,0,0,0.85);
  border-radius: 16px 16px 0 0;
  padding: 8px 0;
  display: flex;
  flex-direction: column;
  gap: 8px;
  min-width: 160px;
  pointer-events: auto;
}
.modal {
  position: fixed;
  left: 0; top: 0; right: 0; bottom: 0;
  background: rgba(0,0,0,0.7);
  display: flex;
  align-items: center;
  justify-content: center;
  pointer-events: auto;
}
.modal-content {
  background: #fff;
  border-radius: 24px;
  padding: 32px;
  min-width: 320px;
  max-width: 90vw;
  min-height: 200px;
  max-height: 80vh;
  display: flex;
  flex-direction: column;
  align-items: center;
  gap: 24px;
  position: relative;
}
.bet-scroll {
  overflow-y: auto;
  max-height: 60vh;
}
.close-info {
  position: absolute;
  right: 24px;
  bottom: 24px;
}
@media (max-width: 900px) {
  .ui-bar { min-height: 60px; }
  .ui-btn { padding: 10px 14px; font-size: 1rem; }
  .modal-content { padding: 16px; }
}
@media (max-width: 450px) and (orientation: portrait) {
  .ui-bar { min-height: 44px; }
  .ui-left, .ui-center, .ui-right { gap: 6px; }
  .ui-btn {
    margin: 0 2px;
    padding: 16px 16px;
    font-size: 1.15rem;
    min-width: 48px;
    min-height: 48px;
    border-radius: 8px;
  }
  .minus-btn, .plus-btn {
    min-width: 36px;
    min-height: 36px;
    padding: 10px 12px;
    font-size: 1.05rem;
  }
  .bet-btn { padding: 12px 14px; font-size: 1.1rem; }
  .play-btn { margin-right: 5vh; }
}
</style>
