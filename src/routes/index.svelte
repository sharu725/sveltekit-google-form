<script>
  let submitStatus;
  const submitForm = async (data) => {
    submitStatus = "submitting";
    const formData = new FormData(data.currentTarget);

    const res = await fetch("contact.json", {
      method: "POST",
      body: formData,
    });

    const { message } = await res.json();
    submitStatus = message;
  };
</script>

{#if submitStatus == "submitting"}
  <p>Submitting...</p>
{:else if submitStatus == "failed"}
  <p>Form submission failed</p>
{:else if submitStatus == "success"}
  <p>Form submission successful</p>
{:else}
  <form on:submit|preventDefault={submitForm}>
    <div>
      <label for="">
        Name
        <input type="text" name="name" />
      </label>
    </div>
    <div>
      <label for="">
        Email
        <input type="email" name="email" />
      </label>
    </div>
    <div>
      <input type="submit" />
    </div>
  </form>
{/if}

<style>
  div {
    margin-bottom: 0.5em;
  }
</style>
