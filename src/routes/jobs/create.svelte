<script>   
    import { goto } from '@sapper/app';

    let title;
    let salary;
    let details;

    const handleSubmit = async () => {
        if (title && salary && details){
            const res = await fetch('jobs.json', {
                method: 'POST',
                headers: { 'Content-Type': 'application/json' },
                body: JSON.stringify({ title, salary, details})
            });

            const updatedJobs =  await res.json();
            console.log(updatedJobs);
            goto('/jobs')
        }
    }

</script>




<style>
    h2{
      text-align: center;
    }
    form {
      max-width: 360px;
      margin: 40px auto;
      text-align: center;
    }
    input, textarea {
      display: block;
      width: 100%;
      padding: 10px;
      font-family: arial;
      margin: 10px auto;
      border: 1px solid #eee;
      border-radius: 8px;
    }
</style>


<div>
    <a href="/jobs">- Back to Jobs</a>
</div>

<h2>Add a new job</h2>
<form on:submit|preventDefault={ handleSubmit }>
    <input bind:value={ title } type="text" placeholder="Job Title" required>
    <input bind:value={ salary } type="number" placeholder="Salary" required>
    <textarea bind:value={ details } placeholder="Job Details" required></textarea>
    <button class="btn">Add new job</button>

</form>
