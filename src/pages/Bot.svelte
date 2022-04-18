<script>
  import { onMount } from 'svelte'

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
  })
</script>

<section id="bot">
  <h1 class="display-1 text-center mt-3">Audit Bot</h1>

  <div class="container-fluid px-5 mt-3">
    <div class="row align-items-center">
      <div class="col-md-6 col-lg-3">
        <input type="text" id="auditorName" class="form-control" placeholder="Enter your name">
      </div>
      <div class="mt-3 mt-md-0 col-md-6 col-lg-3">
        <input type="text" id="tutorName" class="form-control" placeholder="Enter the tutor's name">
      </div>
      <div class="mt-3 col-md-6 col-lg-3 mt-lg-0">
        <input type="text" id="sessionNumber" class="form-control" placeholder="Enter the session number">
      </div>
      <div class="mt-3 col-md-6 col-lg-3 mt-lg-0">
        <input type="date" id="date" class="form-control" min="2022-01-01" max={today}>
      </div>
      <div class="mt-3 col-md-6 offset-md-3">
        <input type="submit" class="btn btn-primary form-control" value="Next">
      </div>
    </div>
  </div>
</section>
