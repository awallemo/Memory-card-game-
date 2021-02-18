var listcards = [];
var flippedList = [];
let counter = 0;
let currentplayer = 1;
let p1 = 0;
let p2 = 0;
let flippet = 0;


 
class Card {
    constructor(i, img) {
        this.img_id = i;
        this.img = img;
        this.flipped = false;
        this.removed = false;
    }
}
 
 
function shuffle(a) {
    var j, x, i;
    for (i = a.length - 1; i > 0; i--) {
        j = Math.floor(Math.random() * (i + 1));
        x = a[i];
        a[i] = a[j];
        a[j] = x;
    }
    return a;
}



//Creating cards 
for (let i = 0; i < 8; i++) {
    let newcard1 = new Card(i, 'images/' + i + '.png');
    let newcard2 = new Card(i, 'images/' + i + '.png');
    listcards.push(newcard1)
    listcards.push(newcard2)
}
shuffle(listcards);
 
var card = new Vue({
    el: "#app",
    template: `
    <div>
    <div class = "players"> Player1: {{p1}}
    </div>
    <div class = "flipped">Flips: {{flippet}} 
    </div>
    <div class = "player2"> Player 2:{{p2}} 
    </div>
    
    
    <div id="bigcardboard" >
        <div v-for="card in listcards" class="outer" v-on:click="flip(card)">
            <div class="card front"  v-bind:style="{ transform: card.flipped? 'none': 'rotateY(180deg)', display: card.removed ? 'none': ''}">
                <img :src="card.img">
            </div>
            <div class="card back" v-bind:style="{ transform: card.flipped? 'rotateY(180deg)': 'none', display: card.removed ? 'none': '' }"></div>
        </div>
    </div>
    </div>
    `,
    data: {
        flipped: false,
        listcards,
        flippet,
        flippedList,
        removed: false,
        currentplayer,
        p1,
        p2    
 
    },
    methods: {
        flip: function (card) {
            if (card.flipped) {
                card.flipped = false;
            }
            else {
                card.flipped = true;
                flippedList.push(card);
                this.cardChecker()
        
            }
        
        }, cardChecker: function(){
            if(flippedList.length == 1){
                console.log(flippedList);
            }
            if(flippedList.length == 2){
                card1 = flippedList[0];
                card2 = flippedList[1];
        
                if (card1.flipped == true && card2.flipped == true){
                    
                    setTimeout(function(){card1.flipped = false},700);
                    setTimeout(function(){card2.flipped = false}, 700);
                }
        
                counter +=1;
                console.log(flippedList);
                if(card1.img_id == card2.img_id){
                    this.flippet ++;
                    console.log("Correct");
                    setTimeout(function(){card1.removed = true},700);
                    setTimeout(function(){card2.removed = true},700);
                    if (currentplayer == 1){
                        this.p1 ++;
                        if(this.p1 + this.p2 == 8){
                            if(this.p1 > this.p2){
                            window.alert("Gratulerer du vant p1")
                            }else{
                                window.alert("Gratulerer du vant p2")
                            }
                        }
                    }else if (currentplayer == 2) {
                        this.p2 ++;
                        if(this.p1 + this.p2 == 8){
                            if(this.p1 > this.p2){
                            window.alert("Gratulerer du vant p1")
                            }else{
                                window.alert("Gratulerer du vant p2")
                            }
                        }
                    }
                    flippedList = []
                    
                }else{
                    this.flippet ++;
                    if(currentplayer == 1){
                        currentplayer = 2;
                    }else if (currentplayer ==2){
                        currentplayer = 1;
                    }
                    flippedList = []       
                }
                 
            }
        }
        }
    }
    
);


 
/*function cardChecker(){
    
    if(flippedList.length == 1){
        console.log(flippedList);
    }
    if(flippedList.length == 2){
        card1 = flippedList[0];
        card2 = flippedList[1];

        if (card1.flipped == true && card2.flipped == true){
            
            setTimeout(function(){card1.flipped = false},700);
            setTimeout(function(){card2.flipped = false}, 700);
        }

        counter +=1;
        console.log(flippedList);
        if(card1.img_id == card2.img_id){
            console.log("Correct");
            setTimeout(function(){card1.removed = true},700);
            setTimeout(function(){card2.removed = true},700);
            if (currentplayer == 1){
                p1 ++;
            }else if (currentplayer == 2) {
                p2 ++;
            }
            flippedList = []
            
        }else{
            if(currentplayer == 1){
                currentplayer = 2;
            }else if (currentplayer ==2){
                currentplayer = 1;
            }
            flippedList = []       
        }
         
    }
}*/
 
 
