
<!DOCTYPE html>
<html>
<head>
    <title>Voting System</title>
</head>
<body>

<h2>🗳 Voting System</h2>

<label>Enter Voter ID:</label><br>
<input type="text" id="voterId"><br><br>

<label>Select Candidate:</label><br>
<select id="candidate">
    <option value="0">Alice</option>
    <option value="1">Bob</option>
    <option value="2">Charlie</option>
</select><br><br>

<button onclick="vote()">Vote</button>
<button onclick="showResults()">Show Results</button>

<h3 id="message"></h3>

<script>
let candidates = ["Alice", "Bob", "Charlie"];
let votes = [0, 0, 0];
let votedUsers = [];

function isValidVoterID(user) {
    if (user.length !== 10) return false;
    if (!/^[A-Za-z]{3}/.test(user)) return false;
    if (!/[0-9]{7}$/.test(user)) return false;
    return true;
}

function vote() {
    let user = document.getElementById("voterId").value;
    let choice = document.getElementById("candidate").value;

    if (!isValidVoterID(user)) {
        document.getElementById("message").innerText = "❌ Invalid Voter ID!";
        return;
    }

    if (votedUsers.includes(user)) {
        document.getElementById("message").innerText = "❌ Already voted!";
        return;
    }

    votes[choice]++;
    votedUsers.push(user);

    document.getElementById("message").innerText = "✅ Vote cast successfully!";
}

function showResults() {
    let result = "📊 Results:\n";

    for (let i = 0; i < candidates.length; i++) {
        result += candidates[i] + ": " + votes[i] + " votes\n";
    }

    let maxVotes = Math.max(...votes);
    let winners = [];

    for (let i = 0; i < votes.length; i++) {
        if (votes[i] === maxVotes) {
            winners.push(candidates[i]);
        }
    }

    if (winners.length > 1) {
        result += "\n🤝 Tie between:\n";
        for (let name of winners) {
            result += name + "\n";
        }
    } else {
        result += "\n🏆 Winner: " + winners[0];
    }

    document.getElementById("message").innerText = result;
}
</script>

</body>
</html>
