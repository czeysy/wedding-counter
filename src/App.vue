<template>
  <div class="app">
    <div class="overlay">
      <div class="counter">In {{ daysLeft }} Days</div>
      <div class="header-text">Katie & Brownie's Wedding</div>
    </div>
    <a
      class="calendar-button"
      :href="googleCalendarLink"
      target="_blank"
      rel="noopener noreferrer"
    >
      Save the date!
    </a>
  </div>
</template>

<script>
export default {
  data() {
    return {
    targetDate: new Date('2025-10-14T00:00:00'), // Countdown target date
    daysLeft: 0,
  };
  },
  mounted() {
    this.calculateDaysLeft();
    this.constructGoogleCalendarLink();
    setInterval(this.calculateDaysLeft, 86400000); // Update every 24 hours
  },
  methods: {
    calculateDaysLeft() {
     const today = new Date();
     const timeDiff = this.targetDate - today;
     this.daysLeft = Math.floor(timeDiff / (1000 * 60 * 60 * 24)); // Use Math.floor for exact days left
   },
    constructGoogleCalendarLink() {
      const eventTitle = encodeURIComponent("Katie & Brownie's Wedding");
      const eventDetails = encodeURIComponent("Join us in celebrating Katie & Brownie's special day!");
      const eventLocation = encodeURIComponent("To Be Announced");

      // Format for all-day event on 14/10/2025
      const startDate = '20251014'; // Start date in YYYYMMDD format
      const endDate = '20251015'; // End date is the day after to signify an all-day event

      this.googleCalendarLink = `https://calendar.google.com/calendar/render?action=TEMPLATE&text=${eventTitle}&dates=${startDate}/${endDate}&details=${eventDetails}&location=${eventLocation}&sf=true&output=xml`;
    },
  },
};
</script>

<style>
html, body {
  margin: 0;
  padding: 0;
  overflow: hidden; /* Prevents scrolling */
  width: 100vw;
  height: 100vh;
}

.app {
  background-image: url('@/assets/image_123650291.JPG'); /* Path to your new image */
  background-size: cover; /* Ensures the image covers the entire page */
  background-repeat: no-repeat;
  background-position: center;
  background-color: #000; /* Fallback color to blend with the image */
  width: 100vw; /* Full width */
  height: 100vh; /* Full height */
  display: flex;
  flex-direction: column;
  justify-content: flex-end; /* Moves content to the bottom */
  align-items: center;
  position: relative;
}

.overlay {
  width: 100%;
  display: flex;
  flex-direction: column;
  align-items: center;
  padding-bottom: 30px; /* Adds space from the bottom */
}

.header-text {
  color: white;
  font-size: 48px; /* Slightly smaller font size */
  font-family: 'Times New Roman', serif; /* Reverting to a standard serif font */
  font-weight: bold; /* Keeps the text bold */
  text-align: center;
  margin-top: 20px;
}

.counter {
  color: white;
  font-size: 36px; /* Slightly smaller font for counter */
  font-family: 'Times New Roman', serif; /* Matches the main text */
  font-weight: normal; /* Not as bold as the main text */
  text-align: center;
}

.calendar-button {
  position: absolute;
  top: 20px;
  right: 20px;
  padding: 10px 20px;
  font-size: 16px;
  background: linear-gradient(145deg, rgba(128, 0, 32, 0.7), rgba(105, 105, 105, 0.7)); /* Gradient of burgundy to silver */
  color: #e0e0e0; /* Soft silver text */
  border: 1px solid rgba(0, 0, 0, 0.8); /* Black border for a subtle outline */
  border-radius: 10px; /* Rounded corners */
  cursor: pointer;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.2); /* Slight shadow for depth */
  text-decoration: none; /* Remove underline for the link */
  transition: background 0.3s, border-color 0.3s, color 0.3s, box-shadow 0.3s; /* Smooth transition */
}

.calendar-button:hover {
  background: linear-gradient(145deg, rgba(128, 0, 32, 0.9), rgba(169, 169, 169, 0.9)); /* Darker gradient for hover */
  border-color: rgba(255, 255, 255, 0.8); /* Silver border on hover */
  color: #ffffff; /* Brighter text color on hover */
  box-shadow: 0 6px 12px rgba(0, 0, 0, 0.3); /* Enhanced shadow for hover */
}
</style>
