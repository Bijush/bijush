<!DOCTYPE html>
<html lang="en">
<head>
<meta charset="UTF-8" />
<meta name="viewport" content="width=device-width, initial-scale=1" />
<title>Bijush's GitHub Projects</title>
<style>
  body {
    font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;
    max-width: 900px;
    margin: 30px auto;
    padding: 0 20px;
    background: #f7f9fc;
    color: #333;
  }
  h1 {
    text-align: center;
    margin-bottom: 10px;
  }
  #repoList {
    list-style: none;
    padding: 0;
  }
  #repoList li {
    background: white;
    margin: 10px 0;
    padding: 15px 20px;
    border-radius: 8px;
    box-shadow: 0 3px 7px rgb(0 0 0 / 0.1);
    transition: box-shadow 0.3s ease;
  }
  #repoList li:hover {
    box-shadow: 0 6px 15px rgb(0 0 0 / 0.15);
  }
  a.repo-link {
    font-weight: 600;
    color: #0366d6;
    text-decoration: none;
  }
  a.repo-link:hover {
    text-decoration: underline;
  }
  .desc {
    margin-top: 6px;
    font-size: 0.9rem;
    color: #555;
  }
</style>
</head>
<body>
  <h1>Bijush's GitHub Repositories</h1>
  <ul id="repoList">
    <li>Loading repositories...</li>
  </ul>

  <script>
    async function fetchRepos() {
      const username = 'Bijush'; // Your GitHub username
      const repoListEl = document.getElementById('repoList');
      repoListEl.innerHTML = '';

      try {
        const res = await fetch(`https://api.github.com/users/${username}/repos?sort=updated&per_page=100`);
        if (!res.ok) throw new Error(`GitHub API error: ${res.status}`);

        const repos = await res.json();

        if (repos.length === 0) {
          repoListEl.innerHTML = '<li>No public repositories found.</li>';
          return;
        }

        repos.forEach(repo => {
          // If you host pages in the repo, the URL is https://<username>.github.io/<repo>
          // Check if the repo has GitHub Pages enabled or just link to repo itself
          const pagesUrl = `https://${username.toLowerCase()}.github.io/${repo.name}/`;

          const li = document.createElement('li');

          // Create repo link - prefer GitHub Pages if homepage exists else repo html_url
          const repoLink = document.createElement('a');
          repoLink.className = 'repo-link';
          repoLink.href = pagesUrl;
          repoLink.target = '_blank';
          repoLink.rel = 'noopener noreferrer';
          repoLink.textContent = repo.name;

          // For a better fallback, test if the GitHub Pages URL exists is more complex, so we just link to pagesUrl.
          // You can manually update if some repos don't have GitHub Pages.

          li.appendChild(repoLink);

          if (repo.description) {
            const desc = document.createElement('p');
            desc.className = 'desc';
            desc.textContent = repo.description;
            li.appendChild(desc);
          }

          repoListEl.appendChild(li);
        });
      } catch (error) {
        repoListEl.innerHTML = `<li>Error loading repositories: ${error.message}</li>`;
      }
    }

    fetchRepos();
  </script>
</body>
</html>


<!--
**Bijush/bijush** is a ✨ _special_ ✨ repository because its `README.md` (this file) appears on your GitHub profile.

Here are some ideas to get you started:

- 🔭 I’m currently working on ...
- 🌱 I’m currently learning ...
- 👯 I’m looking to collaborate on ...
- 🤔 I’m looking for help with ...
- 💬 Ask me about ...
- 📫 How to reach me: ...
- 😄 Pronouns: ...
- ⚡ Fun fact: ...
-->
