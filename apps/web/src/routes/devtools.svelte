<script lang="typescript" context="module">
  export async function preload() {
      if (!process.browser) {
          const fs = require("fs")
          const util = require("util")
          const readdir = util.promisify(fs.readdir)

          return {
              testSkills: (await readdir("./src/courses/test/challenges")).map(
                  (fname) => fname.split(".")[0]
              ),
          }
      }
  }
</script>

<script lang="typescript">
  import NavBar from "../components/NavBar"
  import Content from "lluis/Content"

  export let testSkills = []
</script>

<svelte:head>
  <title>LibreLingo - Development</title>
</svelte:head>

<NavBar dark />

<section class="section">
  <div class="container">
    <Content>
      <h1 class="is-size-1">Development tools</h1>
      <h2 class="is-size-2">Test pages</h2>
      <ul>
        <li><a href="/course/test">Test course</a></li>
        {#each testSkills as testSkill}
          <li>
            <a target="_blank" href="/course/test/skill/{testSkill}">
              Test skill:
              <b>{testSkill}</b>
            </a>
          </li>
        {/each}
      </ul>
    </Content>
  </div>
</section>
