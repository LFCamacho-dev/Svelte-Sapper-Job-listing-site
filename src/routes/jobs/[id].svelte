<script context="module">
import { HtmlTagHydration } from "svelte/internal";


	export async function preload(page, session) {
		
        const { id } = page.params;

        const res = await this.fetch(`jobs/${id}.json`);

        if(res.status == 200){
            const job = await res.json();
            return { job }
        }

        if(res.status == 404){
            const { error } = await res.json();
            this.error(404, error);
        }
        


	}

</script>
    
<script>
    export let job;
    
</script>

<style></style>

<div>
    <a href="/jobs">- Back to Jobs</a>
</div>
&nbsp;

<div class="job">
    <h2>{ job.title } </h2>
    <small><i>Job ID# { job.id }</i></small>
    <p>Salary of: ${job.salary}</p>
    <p>Job Description: { job.details }</p>
</div>