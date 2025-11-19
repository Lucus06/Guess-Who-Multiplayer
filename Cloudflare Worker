js
this.roomState.log.push(`${senderName} asked: ${msg.text}`);
await this.saveAndBroadcastState();
break;
case 'toggleEliminate':
const idx = msg.index;
if(typeof idx === 'number' && this.roomState.board[idx]){
this.roomState.board[idx].eliminated = !this.roomState.board[idx].eliminated;
this.roomState.log.push(`${senderName} toggled ${this.roomState.board[idx].name}`);
await this.saveAndBroadcastState();
}
break;
case 'guess':
this.roomState.log.push(`${senderName} made a guess (game end flow not enforced)`);
await this.saveAndBroadcastState();
break;
case 'reset':
this.roomState.board.forEach(c=>c.eliminated=false);
this.roomState.log.push(`${senderName} reset the board`);
await this.saveAndBroadcastState();
break;
default:
// unknown
break;
}
}


async onClose(clientId){
// remove player
const idx = this.roomState.players.findIndex(p=>p.clientId===clientId);
if(idx>=0){
const name = this.roomState.players[idx].name;
this.roomState.players.splice(idx,1);
this.roomState.log.push(`${name} left`);
await this.saveAndBroadcastState();
}
this.clients.delete(clientId);
}


async saveAndBroadcastState(){
try{ await this.state.storage.put('roomState', this.roomState); }catch(e){/*ignore*/}
const payload = JSON.stringify({ type:'state', state: this.roomState });
for(const [cid, cl] of this.clients.entries()){
try{ cl.ws.send(payload); }catch(e){ /* ignore send errors */ }
}
}


broadcast(text){
this.roomState.log.push(text);
this.saveAndBroadcastState();
}
}
