jsx
<button onClick={createAndJoin}>Create room</button>
<input placeholder="room id" value={room} onChange={e=>setRoom(e.target.value)} />
<button onClick={joinRoom}>Join room</button>
</div>
<p style={{marginTop:10}}>Rooms are simple short ids. Share with friends to join.</p>
</div>
)
}


// Game UI when connected and have state
return (
<div className="game-root">
<header>
<h2>Room: {state.roomId} — You: {name} — Turn: {state.turn}</h2>
<div>Players: {state.players.map(p=>p.name).join(', ')}</div>
</header>


<main>
<div className="board">
{state.board.map((c, i)=> (
<div key={i} className={`card ${c.eliminated? 'dead':''}`} onClick={()=>sendAction({type:'toggleEliminate', index:i})}>
<div className="avatar">{c.name[0]}</div>
<div className="label">{c.name}</div>
</div>
))}
</div>


<section className="controls">
<input id="q" placeholder="Ask a yes/no question" />
<button onClick={()=>{
const q = document.getElementById('q').value.trim();
if(q) sendAction({type:'ask', text:q});
}}>Ask</button>


<button onClick={()=>sendAction({type:'guess'})}>Guess (end turn)</button>
<button onClick={()=>sendAction({type:'reset'})}>Reset Board</button>
</section>


<section className="log">
<h4>Log</h4>
{state.log.slice().reverse().map((l,idx)=>(<div key={idx}>{l}</div>))}
</section>
</main>
</div>
)
}
