<script>
    import { onMount, onDestroy } from 'svelte';
    const targetDate = new Date('2024-11-20T18:00:00');
    
    let days = 0;
    let hours = 0;
    let minutes = 0;
    let seconds = 0;
    let timerInterval;
  
    function calculateTimeLeft() {
      const total = targetDate - new Date();
      
      if (total <= 0) {
        clearInterval(timerInterval);
        return;
      }
  
      days = Math.floor(total / (1000 * 60 * 60 * 24));
      hours = Math.floor((total % (1000 * 60 * 60 * 24)) / (1000 * 60 * 60));
      minutes = Math.floor((total % (1000 * 60 * 60)) / (1000 * 60));
      seconds = Math.floor((total % (1000 * 60)) / 1000);
    }
  
    onMount(() => {
      calculateTimeLeft();
      timerInterval = setInterval(calculateTimeLeft, 1000);
    });
  
    onDestroy(() => {
      if (timerInterval) {
        clearInterval(timerInterval);
      }
    });
  
    // Helper function to add leading zeros
    function padNumber(num) {
      return num.toString().padStart(2, '0');
    }
  </script>
  
  <div class="countdown-container">
    <div class="countdown-item">
      <span class="number">{days}</span>
      <span class="label">Days</span>
    </div>
    <div class="countdown-item">
      <span class="number">{padNumber(hours)}</span>
      <span class="label">Hours</span>
    </div>
    <div class="countdown-item">
      <span class="number">{padNumber(minutes)}</span>
      <span class="label">Minutes</span>
    </div>
    <div class="countdown-item">
      <span class="number">{padNumber(seconds)}</span>
      <span class="label">Seconds</span>
    </div>
  </div>
  
  <style>
    .countdown-container {
      display: flex;
      justify-content: center;
      gap: 2rem;
      padding: 2rem;
      font-family: Arial, sans-serif;
    }
  
    .countdown-item {
      display: flex;
      flex-direction: column;
      align-items: center;
      min-width: 100px;
    }
  
    .number {
      font-size: 3rem;
      font-weight: bold;
      color: #333;
    }
  
    .label {
      font-size: 1rem;
      color: #666;
      text-transform: uppercase;
      margin-top: 0.5rem;
	}
</style>
