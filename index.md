<!DOCTYPE html>
<html>
   <head>
      <title>HTML Meta Tag</title>
       </head>
   <body>
     function repositories(username) {
  return fetch(`https://raw.githubusercontent.com/covid19india/api/gh-pages/raw_data.json`)
    .then((response) => {
      return response.json()
    })
    .then(json => {
      return json
    })
    .catch((err) => {
      console.log('Fetch Error :-S', err);
    });
}

const getRepos = async(username) => {
  const ret = await repositories(username)
  return ret
}

(async function() {
  const repos = await getRepos('gegeke')
  // now you have the repositories in the repos const - from here,
  // you can work with it
  // console.log('getRepos:', repos)

  // destructuring the repos array
  // rep1 - first element
  // rep2 - second element
  // repRest - rest of elements
  const [rep1, rep2, ...repRest] = repos
  addTwoRows([rep1, rep2])
  addSelectOptions(repRest)
})();

const addTwoRows = (rows) => {
  rows.forEach(e => {
    const tbody = document.querySelector('#gitTable tbody')
    const tr = document.createElement('tr')
    tr.innerHTML = rowHtml(e)
    tbody.appendChild(tr)
  })
}

const rowHtml = row => {
  html = ''
  html += `<td>${row.name}</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td>`
  return html
}

const addSelectOptions = (arr) => {
  const dropdown = document.getElementById('selectDD')
  dropdown.innerHTML = selectHtml(arr)
}

const selectHtml = arr => {
  return arr.map(e => `<option>${e.name}</option>`).join('')
}




The snippet below

    fetches the Github repo

    adds two rows to the table (names only)

    adds the rest to the dropdown

function repositories(username) {
  return fetch(`https://api.github.com/users/${username}/repos`)
    .then((response) => {
      return response.json()
    })
    .then(json => {
      return json
    })
    .catch((err) => {
      console.log('Fetch Error :-S', err);
    });
}

const getRepos = async(username) => {
  const ret = await repositories(username)
  return ret
}

(async function() {
  const repos = await getRepos('gegeke')
  // now you have the repositories in the repos const - from here,
  // you can work with it
  // console.log('getRepos:', repos)

  // destructuring the repos array
  // rep1 - first element
  // rep2 - second element
  // repRest - rest of elements
  const [rep1, rep2, ...repRest] = repos
  addTwoRows([rep1, rep2])
  addSelectOptions(repRest)
})();

const addTwoRows = (rows) => {
  rows.forEach(e => {
    const tbody = document.querySelector('#gitTable tbody')
    const tr = document.createElement('tr')
    tr.innerHTML = rowHtml(e)
    tbody.appendChild(tr)
  })
}

const rowHtml = row => {
  html = ''
  html += `<td>${row.name}</td><td></td><td></td><td></td><td></td><td></td><td></td><td></td><td></td>`
  return html
}

const addSelectOptions = (arr) => {
  const dropdown = document.getElementById('selectDD')
  dropdown.innerHTML = selectHtml(arr)
}

const selectHtml = arr => {
  return arr.map(e => `<option>${e.name}</option>`).join('')
}

table,
th,
td {
  border: 1px solid black;
  border-collapse: collapse;
}

th,
td {
  padding: 5px;
}

<table id="gitTable">
  <thead>
    <tr>
      <th>Repository<br>Name:</th>
      <th>Timestamps:<br>Created &<br>Updated</th>
      <th>Size</th>
      <th>Number<br>of forks</th>
      <th>Number<br>of<br>open<br>issues</th>
      <th>HTML URL</th>
      <th>List of Languages<br>Used and URL</th>
      <th>Downloads</th>
      <th>Branches</th>
    </tr>
  </thead>
  <tbody></tbody>
</table>
<div>
  Please select a third row :
  <select id="selectDD" onchange="">
  </select>
</div>
<div>
  <button onclick="">Refresh</button>
</div>
   </body>
</html>
