<script>
  import { onMount } from 'svelte'

  let isLiveHelp = true
  let data = {
    auditor: '',
    tutor: '',
    session: '',
    date: '',
    topic: ''
  }

  let today = ''
  onMount(() => {
    const date = new Date()
    const y = date.getFullYear()
    let m = date.getMonth() + 1
    const d = date.getDate()

    if (m < 10) {
      m = "0" + m
    }
    today = `${y}-${m}-${d}`
    data.date = today
  })

  function handleSubmit() {

  }
</script>

<section id="bot">
  <h1 class="display-1 text-center mt-3">Audit Bot</h1>

  <form on:submit={handleSubmit}>
    <div class="container-fluid px-5 mt-3">
      <div class="row align-items-center">
        <div class="col-md-6 col-lg-3">
          <input bind:value={data.auditor} type="text" id="auditorName" class="form-control" placeholder="Enter your name">
        </div>
        <div class="mt-3 mt-md-0 col-md-6 col-lg-3">
          <input type="text" id="tutorName" bind:value={data.tutor} class="form-control" placeholder="Enter the tutor's name">
        </div>
        <div class="mt-3 col-md-6 col-lg-3 mt-lg-0">
          <input type="text" id="sessionNumber" bind:value={data.session} class="form-control" placeholder="Enter the session number">
        </div>
        <div class="mt-3 col-md-6 col-lg-3 mt-lg-0">
          <input type="date" id="date" class="form-control" bind:value={data.date} min="2022-01-01" max={today}>
        </div>
        <div class="col-12 mt-3">
          <div class="d-inline-block">
            Was this a Live Help Session?
          </div>
          <div class="col-12 form-check mt-1 mt-md-0 d-inline-block">
            <input bind:group={isLiveHelp} value={true} class="form-check-input" type="radio" name="live-help" id="live-help-y" checked>
            <label class="form-check-label" for="live-help-y">
              Yes
            </label>
          </div>
          <div class="form-check d-inline-block">
            <input bind:group={isLiveHelp} value={false} class="form-check-input" type="radio" name="live-help" id="live-help-n">
            <label class="form-check-label" for="live-help-n">
              No
            </label>
          </div>
        </div>
        {#if !isLiveHelp}
          <div>
            <input type="text" bind:value={data.topic} id="topic" class="form-control mt-3" placeholder="Enter the topic name">
          </div>
        {/if}
        <div class="mt-3 col-md-6 offset-md-3">
          <input type="submit" class="btn btn-primary form-control" value="Next">
        </div>
      </div>
    </div>
  </form>
</section>
