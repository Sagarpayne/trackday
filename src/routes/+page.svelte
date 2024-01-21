<!-- App.svelte -->
<script>
    import { onMount } from 'svelte';
  
    let activities = [
      { name: 'Gym', clicked: false },
      { name: 'Breakfast', clicked: false },
      { name: 'Snack 1', clicked: false },
      { name: 'Snack 2', clicked: false },
      { name: 'Book Read', clicked: false },
      { name: 'Study', clicked: false },
      { name: 'Walk', clicked: false },
      { name: 'Exercise', clicked: false },
      { name: 'Dinner', clicked: false },
    ];
  
    let formData = {};
    let todayDate = new Date().toLocaleDateString();
  
    function handleButtonClick(index) {
      activities[index].clicked = !activities[index].clicked;
    }
  
    function handleReset() {
      activities.forEach((activity) => {
        activity.clicked = false;
      });
      formData = {};
    }
  
    function handleSubmit() {
      const currentDate = new Date();
      activities.forEach(({ name, clicked }) => {
        formData = { ...formData, [name]: clicked ? 'Yes' : 'No' };
      });
  
      formData = { ...formData, currentDate: currentDate.toLocaleString() };
  
      console.log('Form Data:', formData);
    }
  
    // Log data onMount (for demonstration purposes)
    onMount(() => {
      console.log('Current data:', activities);
    });
  </script>
  
  <main>
    <div class="center-container">
      <h1>Trackday</h1>
      <p class="date">{todayDate}</p>
  
      {#each activities as { name, clicked }, index}
        <div class="activity">
          <button
            on:click={() => handleButtonClick(index)}
            style="background-color: {clicked ? 'green' : 'red'}"
          >
            {name}
          </button>
        </div>
      {/each}
  
      <div class="buttons">
        <button on:click={handleSubmit} style="background-color: goldenrod;">
          Submit
        </button>
        <button on:click={handleReset} style="background-color: goldenrod;">
          Reset
        </button>
      </div>
  
      {#if Object.keys(formData).length > 0}
        <div class="result">
          <h2>Form Data (JSON):</h2>
          <pre>{JSON.stringify(formData, null, 2)}</pre>
        </div>
      {/if}
    </div>
  </main>
  
  <style>
    main {
      display: flex;
      justify-content: center;
      align-items: center;
      height: 100vh;
    }
  
    .center-container {
      text-align: center;
    }
  
    h1 {
      font-size: 2rem;
      margin-bottom: 1rem;
      color: #333;
    }
  
    .date {
      font-size: 1rem;
      color: #888;
      margin-bottom: 2rem;
    }
  
    .activity {
      margin-top: 1rem;
      display: flex;
      align-items: center;
      justify-content: center;
    }
  
    button {
      padding: 10px;
      font-size: 1rem;
      cursor: pointer;
      color: #fff;
      border: none;
      border-radius: 4px;
      margin: 0 0.5rem;
      transition: background-color 0.3s;
      width:150px;
    }
  
    .buttons {
      margin-top: 1rem;
    }
  
    .result {
      margin-top: 2rem;
      text-align: left;
    }
  
    pre {
      font-family: monospace;
      white-space: pre-wrap;
      text-align: left;
      background-color: #f5f5f5;
      padding: 1rem;
      border-radius: 4px;
      overflow-x: auto;
    }
  </style>
  