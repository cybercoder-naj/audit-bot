<script>
  import { onMount } from 'svelte'

  let data = {
    auditor: '',
    tutor: '',
    session: '',
    date: '',
    topic: '',
    type: 1,
    isLiveHelp: true,
    answers: {
      engagement: true,
      mastery: true,
      active: true,
      safety: false
    },
    safetyMsg: ''
  }

  const questions = [
    ['engagement', 'Did the tutor create an engaging environment?'],
    ['mastery', 'Did the tutor teach the topic without significant errors?'],
    ['active', 'Did the tutor maintain an active learning environment?'],
    ['safety', 'Was there any specific safety concern?']
  ]

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

  function handleSubmit(e) {
    e.preventDefault()
    alert("Check console for submitted data.");
    console.table(data)
  }
</script>

<section id="bot">
  <h1 class="display-1 text-center mt-3">Audit Bot</h1>

  <form on:submit={handleSubmit}>
    <div class="container-fluid px-5 mt-3">
      <div class="row align-items-center">
        <div class="col-md-6 col-lg-3">
          <input bind:value={data.auditor} type="text" id="auditorName" required class="form-control" placeholder="Enter your name">
        </div>
        <div class="mt-3 mt-md-0 col-md-6 col-lg-3">
          <input type="text" id="tutorName" bind:value={data.tutor} class="form-control" required placeholder="Enter the tutor's name">
        </div>
        <div class="mt-3 col-md-6 col-lg-3 mt-lg-0">
          <input type="text" id="sessionNumber" bind:value={data.session} class="form-control" required placeholder="Enter the session number">
        </div>
        <div class="mt-3 col-md-6 col-lg-3 mt-lg-0">
          <input type="date" id="date" class="form-control" bind:value={data.date} min="2022-01-01" required max={today}>
        </div>
        <div class="col-12 mt-3">
          <div class="d-inline-block">
            Was this a Live Help Session?
          </div>
          <div class="col-12 form-check mt-1 mt-md-0 d-inline-block">
            <input bind:group={data.isLiveHelp} value={true} class="form-check-input" type="radio" name="live-help" id="live-help-y" checked>
            <label class="form-check-label" for="live-help-y">
              Yes
            </label>
          </div>
          <div class="form-check d-inline-block">
            <input bind:group={data.isLiveHelp} value={false} class="form-check-input" type="radio" name="live-help" id="live-help-n">
            <label class="form-check-label" for="live-help-n">
              No
            </label>
          </div>
        </div>
        {#if !data.isLiveHelp}
          <div>
            <input type="text" bind:value={data.topic} id="topic" class="form-control mt-3" placeholder="Enter the topic name" required>
          </div>
        {/if}
        <div class="col-12 mt-3">
          <div>
            Choose the best option from below:
          </div>
          <div class="col-12 form-check mt-1 mt-md-0">
            <input bind:group={data.type} value={1} class="form-check-input" type="radio" name="tutor-no-show" id="tutor-no-show" checked>
            <label class="form-check-label" for="tutor-no-show">
              The tutor did not start the meeting.
            </label>
          </div>
          <div class="form-check">
            <input bind:group={data.type} value={2} class="form-check-input" type="radio" name="learner-no-show" id="learner-no-show">
            <label class="form-check-label" for="learner-no-show">
              No learners showed up in the session.
            </label>
          </div>
          <div class="form-check">
            <input bind:group={data.type} value={3} class="form-check-input" type="radio" name="none-of-the-above" id="none-of-the-above">
            <label class="form-check-label" for="none-of-the-above">
              None of the above
            </label>
          </div>
        </div>
        {#if data.type == 3}
          {#each questions as question}
            <div class="col-12 mt-3">
              <div>
                {question[1]}
              </div>
              <div class="col-12 form-check mt-1 mt-md-0">
                <input type="radio" class="form-check-input" bind:group={data.answers[question[0]]} value={true} id={`${question[0]}-y`} checked>
                <label class="form-check-label" for={`${question[0]}-y`}>Yes</label>
              </div>
              <div class="form-check">
                <input type="radio" class="form-check-input" bind:group={data.answers[question[0]]} value={false} id={`${question[0]}-n`}>
                <label class="form-check-label" for={`${question[0]}-n`}>No</label>
              </div>
            </div>
          {/each}
          {#if data.answers.safety}
            <div class="form-group mt-3">
              <label for="safety-message">Detail the safety concern here.</label>
              <textarea class="form-control" id="safety-message" rows="3"></textarea>
            </div>
          {/if}
        {/if}
        <div class="my-3 col-md-6 offset-md-3">
          <input type="submit" class="btn btn-primary form-control" value="Next">
        </div>
      </div>
    </div>
  </form>
</section>
