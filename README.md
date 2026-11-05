if (list.length === 0) {
    container.innerHTML = <div style="text-align:center; padding:20px; color:#64748b;">No questions in this filter.</div>;
    return;
  }

  container.innerHTML = list.map(item => {
    let badge = <span class="badge badge-skip">Unanswered (0.0)</span>;
    if (item.status === 'correct') badge = <span class="badge badge-correct">&#10003; Correct (+1.0)</span>;
    if (item.status === 'wrong') badge = <span class="badge badge-wrong">&#10007; Incorrect (-0.25)</span>;

    return 
      <div class="sol-card ${item.status}">
        <div class="sol-header">
          <span>Q${item.actNum} of 500</span>
          ${badge}
        </div>
        <div style="font-size:13px; font-weight:600; margin-bottom:8px;">${item.q}</div>
        <div style="font-size:12px; margin-bottom:4px;">
          <strong>Your Answer:</strong> ${item.user !== undefined ? letters[item.user] + ') ' + item.o[item.user] : '<span style="color:#64748b;">None</span>'}
        </div>
        <div style="font-size:12px; color:#047857;">
          <strong>Correct Answer:</strong> ${letters[item.a]}) ${item.o[item.a]}
        </div>
        <div class="rationale">
          <strong>Official Rationale:</strong> ${item.e}
        </div>
      </div>
    ;
  }).join('');
}

function setFilter(type, btn) {
  curFilter = type;
  document.querySelectorAll('.filter-btn').forEach(b => b.classList.remove('active'));
  btn.classList.add('active');
  renderSolutions();
}

function backHome() {
  document.getElementById('view-result').classList.add('hidden');
  document.getElementById('view-test').classList.add('hidden');
  document.getElementById('view-home').classList.remove('hidden');
  renderHistory();
}

window.onload = init;
</script>
</body>
</html>