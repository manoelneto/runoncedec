runoncedec
==========

show on console

function decRunOnce(func){
var newFunc = function(){
if (!arguments.callee.runned){
arguments.callee.runned = true;
func.apply(this, arguments); 
}
}
newFunc.runned = false;
newFunc.reset = function(){
newFunc.runned = false;
};
return newFunc;
}
/* função normal que voce cria */
function a(ar){
console.log(ar);
}
a('a'); /* mostra no console => a */
a('a'); /* mostra no console => a */
a('a'); /* mostra no console => a */
a('a'); /* mostra no console => a */
a('a'); /* mostra no console => a */
/* estilo a decorador do python, so que js não da suporte a @(estou enganado?) */
a = decRunOnce(a);
a('b'); /* mostra no console => b */
a('b');
a('b');
a('b');
a('b');
a('b');
a.reset(); /* agora voce pode chamar a função mais uma vez */
a('c'); /* mostra no console => c */
a('c');
a('c');