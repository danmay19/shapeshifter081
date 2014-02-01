
//Shapeshifting mod
//By Amoia5 
 pig=false;
var cow=false;
var sheep=false;
var chicken=false;
var initialized=false;
var count=Math.floor(Math.random() * 9);
var Stickhealth=35;
var dropStick=Math.floor(Math.random() * 25);
var haveStick=false;

function selectLevelHook() {
if(initialized==false) {
ModPE.setItem(470, "blaze_rod", 0, "Shape shifter stick");
ModPE.setItem(471, "potion_bottle_drinkable", 0, "Pig essence");
ModPE.setItem(472, "potion_bottle_drinkable", 0, "Cow essence");
ModPE.setItem(473, "potion_bottle_drinkable", 0, "Sheep essence");
ModPE.setItem(474, "potion_bottle_drinkable", 0, "Chicken essence");
initialized=true;
} 
}

function deathHook(murderer, victim) {
 if(haveStick==false&&dropStick==1){
Level.dropItem(Entity.getX(victim), Entity.getY(victim), Entity.getZ(victim), 1, 470, 1);
haveStick=true;
}
} 

function attackHook(attacker, victim) {
var victimEntity=Entity.getEntityTypeId(victim);
if(getCarriedItem()==470&&victimEntity==12) {
preventDefault();
Level.dropItem(Entity.getX(victim), Entity.getY(victim), Entity.getZ(victim), 1, 471, count);
Stickhealth--;
Entity.setHealth(victim, 0);
}
else if(getCarriedItem()==470&&victimEntity==11) {
preventDefault();
Level.dropItem(Entity.getX(victim), Entity.getY(victim), Entity.getZ(victim), 1, 472, count);
Stickhealth--;
Entity.setHealth(victim, 0);
} 
else if(getCarriedItem()==470&&victimEntity==13) {
preventDefault();
Level.dropItem(Entity.getX(victim), Entity.getY(victim), Entity.getZ(victim), 1, 473, count);
Stickhealth--;
Entity.setHealth(victim, 0);
}
else if(getCarriedItem()==470&&victimEntity==10) {
preventDefault();
Level.dropItem(Entity.getX(victim), Entity.getY(victim), Entity.getZ(victim), 1, 474, count);
Stickhealth--;
Entity.setHealth(victim, 0);
}
}

function useItem(x, y, z, itemId, blockId, side) {
if(itemId==471&&pig==false){
Entity.setRenderType(Player.getEntity(), 8);
pig=true;
cow=false;
sheep=false;
chicken=false
Entity.setMobSkin(Player.getEntity(), "mob/pig.png");
addItemInventory(471, -1, 0);
} 
else if(itemId==470&&pig==true){
Entity.setRenderType(Player.getEntity(), 3);
pig=false;
Entity.setMobSkin(Player.getEntity(),"mob/char.png");
Stickhealth--;
}
else if(itemId==472&&cow==false){
Entity.setRenderType(Player.getEntity(), 7);
Entity.setMobSkin(Player.getEntity(), "mob/cow.png");
cow=true;
pig=false;
sheep=false;
chicken=false;
addItemInventory(472, -1, 0);
}
else if(itemId==470&&cow==true){
Entity.setRenderType(Player.getEntity(), 3);
Entity.setMobSkin(Player.getEntity(), "mob/char.png");
cow=false;
Stickhealth--;
}
else if(itemId==473&&sheep==false){
Entity.setRenderType(Player.getEntity(), 9);
Entity.setMobSkin(Player.getEntity(), "mob/sheep.png");
sheep=true;
cow=false;
pig=false;
chicken=false;
addItemInventory(473, -1, 0);
}
else if(itemId==470&&sheep==true){
Entity.setRenderType(Player.getEntity(), 3);
Entity.setMobSkin(Player.getEntity(), "mob/char.png");
sheep=false;
Stickhealth--;
}
else if(itemId==474&&chicken==false){
Entity.setRenderType(Player.getEntity(), 6);
Entity.setMobSkin(Player.getEntity(), "mob/chicken.png");
addItemInventory(474, -1, 0);
chicken=true;
pig=false;
cow=false;
sheep=false;
}
else if(itemId==470&&chicken==true) {
Entity.setRenderType(Player.getEntity(), 3);
Entity.setMobSkin(Player.getEntity(), "mob/char.png");
chicken=false;
Stickhealth--;
}
}

function modTick() {
var ticks;
if(cow==true||pig==true||sheep==true||chicken==true) {
ticks++;
} 
else if(ticks==1200&&pig==true){
Entity.setRenderType(Player.getEntity(), 3);
Entity.setMobSkin(Player.getEntity(), "mob/char.png");
pig=false;
}
else if(ticks==1200&&cow==true){
Entity.setRenderType(Player.getEntity(), 3);
Entity.setMobSkin(Player.getEntity(), "mob/char.png");
cow=false;
}
else if(ticks==1200&&sheep==true) {
Entity.setRenderType(Player.getEntity(), 3);
Entity.setMobSkin(Player.getEntity(), "mob/char.png");
sheep=false;
}
else if(ticks==1200&&chicken==true) {
Entity.setRenderType(Player.getEntity(), 3);
Entity.setMobSkin(Player.getEntity(), "mob/char.png");
chicken=false;
} 
} 

if(Stickhealth==0) {
addItemInventory(470, -1, 0);
haveStick=false;
}
else if(chicken==true) {
setVelY(Player.getEntity(), -0.1);
}
