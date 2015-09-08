/*
*
* Shiny Hover Canvas
*
* EZ Shiny Canvas Hover Shine made by @Scirodesign for images
*
* OPTIONS:
* -
* -
* -
*
*/
(function( $ ){

'use strict';

//global list of all shiny logos
window.canvasListShinyList = [];

$.fn.shinylogo = function(options){

	var opts = $.extend({
		element : "no img loaded",
		manualDimensions : [],
		topOffset : 0,
		speed : 2000,
		angle : 0,
		doubleShine : true,
		queueStop : true,
		direction : "right",
		leftOffset : 0,
		gradientSizeBuff:0
	}, options);


	return this.each(function(idx, elem){
		//object for easy access to properties and element
		var elemObject = {};


		//if manual options aren't set
		if(!opts.manualDimensions.length > 0){
			var dimensions = analyzeElement(elem);
		}
		else{
			var dimensions = {height:opts.manualDimensions[0],width:opts.manualDimensions[1]};
		}
		elemObject.dimensions = dimensions;
		elemObject.c = new sg_canvasInitializeReplace(elemObject,elem);
		elemObject.gradient = new sl_gradient(elemObject);
		elemObject.timerSafetyNet = null;


		//add to list
		canvasListShinyList.push(elemObject);

		jQuery(elemObject.c.canvas).on("mouseover", function(event){sl_hovered(event, elemObject);});
		draw(elemObject);



	})


function analyzeElement(element,manual){
	var hD = jQuery(element).height();
	var wD = jQuery(element).width();
	var autoDimensions = {height:hD,width:wD};
	return autoDimensions;
}



function sg_canvasInitializeReplace(elemObject,elemToReplace){

	var canvasID = "shinyCanvas" + canvasListShinyList.length;
	this.canvas = document.createElement("canvas");
	this.canvas.id = canvasID;
	this.ctx = this.canvas.getContext("2d");
	this.canvas.width = elemObject.dimensions.width;
	this.canvas.height = elemObject.dimensions.height;

	///hide old image
	jQuery(elemToReplace).css({"display":"none"});
	jQuery(elemToReplace).wrap('<div class="shinylogo '+ canvasID + '"></div>' );
	jQuery(elemToReplace).parent("div").append(this.canvas);
	this.img = elemToReplace;

	return this;
}





function sl_gradient(elemObject){
	this.x = 0;
	this.y = 0;

	this.redrawLogo = function(ctx, x, y, x1, y2, color, imgPassedIn, w, h){


		var img=imgPassedIn;
   		ctx.drawImage(img,0,0);
   		ctx.globalCompositeOperation="source-over";

	};
	this.gradientMove = function(ctx, x, y, x1, y2, color, imgPassedIn, w, h){
		//ctx.fillStyle() = color;
		//ctx.fillRect(x,y,w,h);

		ctx.clearRect(0, 0, w, h);
		ctx.fillRect(0, 0, w, h);

		var img=imgPassedIn;
   			ctx.drawImage(img,0,0);
      	ctx.globalCompositeOperation="source-over";

		var grd = ctx.createLinearGradient(x, y, x1, y2);
      	grd.addColorStop(0, 'rgba(255,255,255,0)');
				if(opts.doubleShine === true){
					grd.addColorStop(0.25, 'rgba(255,255,255,1)');
					grd.addColorStop(0.5, 'rgba(255,255,255,0)');
					grd.addColorStop(0.75, 'rgba(255,255,255,1)');
				}else{
					grd.addColorStop(0.5, 'rgba(255,255,255,1)');
				}
      	grd.addColorStop(1, 'rgba(255,255,255,0)');

       	ctx.fillStyle = grd;
      	ctx.fill();

		ctx.globalCompositeOperation="destination-atop";


	};
}



function sl_hovered(evt, elemObject){
	var direction = "0";

	if(elemObject.timerSafetyNet != null){
		clearTimeout(elemObject.timerSafetyNet);
		elemObject.timerSafetyNet = null;
	}

	if(opts.direction != "right"){
		direction = -1;
	}

	if(opts.queueStop === true){
		jQuery(elemObject.c.canvas).off();
	}

	var gradientX = (elemObject.dimensions.width * 2)  * -1;

	elemObject.timerSafetyNet = setTimeout(function(){
		elemObject.gradient.gradientMove(
			elemObject.c.ctx,
			-elemObject.dimensions.width * 2,
			elemObject.dimensions.height,
			-elemObject.dimensions.width,
			elemObject.dimensions.height + opts.angle,
			null,
			elemObject.c.img,
			elemObject.dimensions.width,
			elemObject.dimensions.height);
			console.log("finished")
	},opts.speed);

	jQuery({ gradientX: (elemObject.dimensions.width * 2)  * -1 }).stop(true,true).animate({ gradientX: elemObject.dimensions.width * 2}, {
    	duration:opts.speed,
    	step: function(now, fx) {
        	elemObject.gradient.gradientMove(
						elemObject.c.ctx,
        		this.gradientX,
        		elemObject.dimensions.height,
        		this.gradientX + elemObject.dimensions.width,
        		elemObject.dimensions.height + opts.angle,
        		null,
        		elemObject.c.img,
        		elemObject.dimensions.width,
        		elemObject.dimensions.height
        		);
    	},
    	done: function(){
    		if(opts.queueStop === true){
    			jQuery(elemObject.c.canvas).on("mouseover", function(event){sl_hovered(event, elemObject);});
    		}
    	}
	})



}





function draw(elemObject){

var startPos = 0;

elemObject.gradient.redrawLogo(elemObject.c.ctx,
    startPos,
    elemObject.dimensions.height,
    startPos + elemObject.dimensions.width,
    elemObject.dimensions.height + opts.angle,
    null,
    elemObject.c.img,
    elemObject.dimensions.width,
    elemObject.dimensions.height,
    true
    );

}



}

}( jQuery ));
