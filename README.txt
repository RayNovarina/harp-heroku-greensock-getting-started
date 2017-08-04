cd /users/raynovarina/sites/AtomProjects/harp/greensock-getting-started/

per: https://greensock.com/jump-start-js
     https://greensock.com/get-started-js#intro

Cloned from my repos:

$ git clone https://github.com/RayNovarina/harp-heroku-mdn-canvas-tutorial.git greensock-getting-started
$ cd greensock-getting-started/

Start harp server:
$ harp server -p 9007

Access via localhost:9007
============================

Modify package.json and Procfile files for Heroku deploy:
  package.json:

    {
      "name": "greensock-tutorial",
      "version": "0.0.1",
      "description": "Harp server App: javascript/greensock-tutorial",
      "dependencies": {
          "harp": "*"
      }
    }

  Procfile:

    web: harp server --port $PORT

At github account, create new repository: harp-heroku-greensock-getting-started and then
locally.
  $ git init
  $ git remote add origin https://github.com/RayNovarina/harp-heroku-greensock-getting-started.git

Create Heroku app:
  $ heroku create harp-greensock-getting-started-94037

$ git remote -v
  heroku  https://git.heroku.com/harp-greensock-getting-started-9403.git (fetch)
  heroku  https://git.heroku.com/harp-greensock-getting-started-9403.git (push)
  origin  https://github.com/RayNovarina/harp-heroku-greensock-getting-started.git (fetch)
  origin  https://github.com/RayNovarina/harp-heroku-greensock-getting-started.git (push)

Deploy changes to github and heroku:
  $ git add .
  $ git commit -am "First Harp + Heroku commit"
  $ git push origin master
  $ git push heroku master

View on Heroku:

  https://harp-greensock-getting-started-9403.herokuapp.com shows:

  Welcome to harp/greensock-getting-started.
  Deployed locally at http://localhost:9007/
  Deployed on Heroku at https://harp-greensock-getting-started-94037.herokuapp.com/

------------------------------

================

  //----------------------------------------------------------------------------
  this.particleFilter = function( rgbChannel, x, y ) {
    //----------------------------------------------------------------------------
    var pixelChannelIntensity = this.getPixelChannelIntensity( x, y, rgbChannel );
    if ( pixelChannelIntensity == 0 ) {
      return { isAccepted: false };
    }
    // Returns null if rejected. Else returns Particle.
    // NOTE: rejected particle locations just remain whatever the canvas
    // background/fill color is.
    if ( pixelChannelIntensity < this.settings.pixelChannelIntensityThreshold ) {
      this.particlesRejectedBecausePixelIntensityLessThanThreshold += 1;
      return { isAccepted: false };
    }
    return {
      isAccepted: true,
      x: x,
      y: y,
      pixelChannelIntensity: pixelChannelIntensity,
    };
  } // end this.particleFilter()

  //----------------------------------------------------------------------------
  this.getPixelChannelIntensity = function( x, y, rgbChannel ) {
    //--------------------------------------------------------------------------
    if (this.settings.imageScale !== 1.0 ) {
        x = Math.round( x / this.settings.imageScale);
        y = Math.round( y / this.settings.imageScale);
    } else {
      x = Math.round( x );
      y = Math.round( y );
    }
    if ( x < 0 || x > this.settings.img.width ||
         y < 0 || y > this.settings.img.height ) {
      this.particlesRejectedBecauseParticleIsOutOfBounds += 1;
      return 0;
    }
    // this.imgData Is a Uint8ClampedArray representing a one-dimensional
    // array containing the data in the RGBA order, with integer values between
    // 0 and 255 (included). sarah.jpg imgData.len = '582400'
    var pixelIndex = ( x + y * this.settings.img.width ) * 4;
    if ( rgbChannel === 'lum') {
			channelRgbValue = this.getPixelLum( pixelIndex );
		} else {
      channelRgbValue = this.imgData[ pixelIndex + this.settings.rgbChannelOffset ]; // get the 'blue' value of the rgba item.
    }
    return 1 - (channelRgbValue / 255);
  } // end getPixelChannelIntensity()

  //----------------------------------------------------------------------------
  this.getPixelLum = function( pixelIndex ) {
    //----------------------------------------------------------------------------
    var r = this.imgData[ pixelIndex + 0 ] / 255;
    var g = this.imgData[ pixelIndex + 1 ] / 255;
    var b = this.imgData[ pixelIndex + 2 ] / 255;
    var max = Math.max( r, g, b );
    var min = Math.min( r, g, b );
    return ( max + min ) / 2;
  } // end getPixelLum()

=================
  //----------------------------------------------------------------------------
  this.createCanvas = function( options ) {
    //--------------------------------------------------------------------------
    console.log( "3) createCanvas() ");
    this.img = new Image();
    this.img.src = options.img.src;

    this.img.onload = function() {
      console.log( "3a) createCanvas() img.onload() Loaded src: " + $this.img.src);
      console.log( "3b) createCanvas() img.width: " + $this.img.width + ". img.height: " + $this.img.height);
      var $imageContainer = createParticles( $this.img, 0, 0, this.id );

      this.imageContainer = $imageContainer;
      $this.imageContainer = $imageContainer;

      var $containerDiv = document.getElementById( 'containerDiv' );
      console.log( "2a) TrrEffect() Created instance with id: '" + this.id +
                   "'. $containerDiv.id: '" + $containerDiv.id + "'*");

      $containerDiv.appendChild( $imageContainer );
    } // end this.img.onload function()

    trrPlugin.createParticles( $this.img, 0, 0, this.id,
    /*2-Resume here when done*/ function( imageContainer ) {
    this.imageContainer = imageContainer;
    this.containerDiv = document.getElementById( 'containerDiv' );
    console.log( "3a) newPhoto()  Created containerDiv.id: '" + this.containerDiv.id + "'*");
    this.containerDiv.appendChild( this.imageContainer );
    callback( this.containerDiv );
    /*2-*/}.bind( this ));/*1-*/}.bind( this );



  } // end: this.createCanvas function()

  //----------------------------------------------------------------------------
  function createParticles( imgObj, left, top, id ) {
    //--------------------------------------------------------------------------
    console.log( "4) createParticles() for id: " + id +
                 ". Image Container left: " + left + ". top: " + top );

		var particlesContainer = document.createElement( "div" );
    particles = makeParticlesFromTrrMap( effectsDataForRender[0].effectsDataAsJSONstring, 80, 20, id );

	  console.log( "4a) createParticles() cols: " + cols + ". rows: " + rows +
                 ". particles[" + particles.length + "]: " +
                 "Image Container left: " + left + ". top: " + top + ". ");
	  particlesContainer.id = $this.id;
	  particlesContainer.style.width = 600 + "px";
	  particlesContainer.style.height = 600 + "px";
	  particlesContainer.style.position = "absolute";
	  particlesContainer.style.left = left + "px";
	  particlesContainer.style.top  = top + "px";
    particlesContainer.style.backgroundColor  = "#E7F1F7";
    particlesContainer.style.border  = "solid 4px green";
    console.log( "4b) createParticles() particlesContainer.width: " +  particlesContainer.style.width +
                 ". particlesContainer.height: " + particlesContainer.style.height +
                 ". Image Container left: " + left + ". top: " + top + ".");

		var canvas;
		var context;
		for( var n = 0; n < particles.length; n++ ) {
		  var particle = particles[ n ];

      canvas = document.createElement( "canvas" );
      context = canvas.getContext("2d");

      // per:
      /* void ctx.drawImage(image, sx, sy, sWidth, sHeight, dx, dy, dWidth, dHeight);
        drawImage Parameters
      image
        An element to draw into the context. The specification permits any canvas image source (CanvasImageSource), specifically, a CSSImageValue, an HTMLImageElement, an SVGImageElement, an HTMLVideoElement, an HTMLCanvasElement, an ImageBitmap, or an OffscreenCanvas.
      dx
        The X coordinate in the destination canvas at which to place the top-left corner of the source image.
      dy
        The Y coordinate in the destination canvas at which to place the top-left corner of the source image.
      dWidth
        The width to draw the image in the destination canvas. This allows scaling of the drawn image. If not specified, the image is not scaled in width when drawn.
      dHeight
        The height to draw the image in the destination canvas. This allows scaling of the drawn image. If not specified, the image is not scaled in height when drawn.
      sx
        The X coordinate of the top left corner of the sub-rectangle of the source image to draw into the destination context.
      sy
        The Y coordinate of the top left corner of the sub-rectangle of the source image to draw into the destination context.
      sWidth
        The width of the sub-rectangle of the source image to draw into the destination context. If not specified, the entire rectangle from the coordinates specified by sx and sy to the bottom-right corner of the image is used.
      sHeight
        The height of the sub-rectangle of the source image to draw into the destination context.
      */
      //if ( !isUseTrrMap ) {
      //  canvas.width = 5;
  		//	canvas.height = 5;
  		//	canvas.style.left = particle.x + "px";
  		//	canvas.style.top = particle.y + "px";
  		//	canvas.style.position = 'absolute';
      //  // void ctx.drawImage( image,  sx,            sy,            sWidth, sHeight, dx, dy, dWidth, dHeight);
      //  context.drawImage(     imgObj, particle.imgX, particle.imgY, 5,      5,       0,  0,  5,      5 );


      // isUseTrrMap
      /*
          canvasBackgroundColor: "#E7F1F7",
          dotsColor: '#70C0EF',
          proxy.ctx.fillStyle = this.options.dotsColor;
          var particle = particles[i];
          if ( this.options.isRenderFromEffectsData ) {
            // particles: [ { x: 123, y: 456, r: 0.1952452452345 } ]
            // Draw a dot centered at postion.x, position.y. Rendered size diameter is 'r'.
            proxy.ctx.beginPath();
            proxy.ctx.arc(particle.x, particle.y, particle.r, 0, TAU);
            proxy.ctx.fill();
            proxy.ctx.closePath();
          }
      */
      canvas.width = 6;
  		canvas.height = 6;
  		canvas.style.left = particle.x + "px";
  		canvas.style.top = particle.y + "px";
  		canvas.style.position = 'absolute';

      context.fillStyle = '#70C0EF';
      context.beginPath();
      context.arc( 0, 0, particle.r, 0, TAU );
      context.fill();
      context.closePath();

      particlesContainer.appendChild(canvas);

    } // end for( var n
   return particlesContainer;
	} // end createParticles()

  //----------------------------------------------------------------------------
  function makeParticlesFromTrrMap( effectsDataAsJSONstring, left, top, id ) {
    //--------------------------------------------------------------------------
    var effectsData = JSON.parse( effectsDataAsJSONstring );
    console.log( "4.1) makeParticlesFromTrrMap() for id: " + id +
                 ". effectsData.particles.len = " + effectsData.particles.length +
                 ". effectsDataAsJSONstring.len = " + effectsDataAsJSONstring.length +
                 ". Canvas Particle left: " + left + ". top: " + top + ".");
    //return effectsData.particles;

    var particles = new Array();
    var effectsDataParticles = effectsData.particles,
        edpParticle = {};

  	for( var i = 0; i < (effectsData.particles.length); i += 1 ) {

        edpParticle = effectsDataParticles[ i ];
  	    particles.push( {
  	        x: edpParticle.x + left,
  	        y: edpParticle.y + top,
            r: edpParticle.r,
  	    });
  	} //end for( var n )
    return particles;
  } // end  makeParticlesFromTrrMap()

  //------------------------------------------------------------------------------
  function getRandom( max, min ) {
    //----------------------------------------------------------------------------
  	return Math.floor( Math.random() * ( 1 + max - min ) + min );
  } // end function getRandom()

  //----------------------------------------------------------------------------
  this.explode = function() {
    //--------------------------------------------------------------------------
		var particleContainer = this.imageContainer;
		console.log( "5) explode() particleContainer: " + particleContainer.id);

		var canvasParticles = $( "#" + particleContainer.id ).children();
    console.log( "5a) explode() " + canvasParticles.length + " canvasParticles.");

		for( var i = 0; i < canvasParticles.length; i++ ) {
			var canvasParticle = canvasParticles.eq(i);
			var randX = getRandom(  300 , -300 );
			var randY = getRandom(  300 , -300 );

			var tmax = TweenMax.to( canvasParticle, 3.0, {
			  left: randX,
				top: randY,
				autoAlpha: 0,
        ease: Power0.easeInOut
			}); // end TweenMax
		} // end for( var i )
	} // end this.explode = function()

  //----------------------------------------------------------------------------
  this.reset = function() {
    //--------------------------------------------------------------------------
    console.log( "6) reset() #" + this.id + ".children().len: " + $( "#" + this.id ).children().length);
    $( "#" + this.id ).empty().remove();
    $( "#container" ).children( "div" ).remove();
    $this.createCanvas();
  } // end this.reset function()
}; // end function TrrEffect()

/*
  // 2) Display default photo.
  trrPlugin.newPhoto( { photoType: "color", photoTag: "meg", imgSrc: './images/meg_CC_422x436.jpg' } ),
  /*1-Resume here when done// function( img ) {
  /*2-//}.bind( this ));/*1-//}.bind( this ));

  // 3) Create canvas particles of selected photo.
  overrides = {
      canvasBackgroundColor: '',
      dotsColor: '',
  };
  trrPlugin.createCanvas( $.extend( {}, defaults, overrides),
  /*2-Resume here when done// function() {
 */
================
<!DOCTYPE html>
<html lang="en">

<head>
  <meta charset="utf-8">
  <meta http-equiv="X-UA-Compatible" content="IE=edge">
  <meta name="viewport" content="width=device-width, initial-scale=1">
  <meta name="description" content="Sandbox for canvas-dots canvas demo." />

  <title>GSAP getting started</title>

    <!-- <link rel="stylesheet" type="text/css" href="css/canvas-bubbles-plume.css"> -->
    <!-- Bootstrap Latest compiled and minified CSS -->
    <!-- link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css" integrity="sha384-BVYiiSIFeK1dGmJRAkycuHAHRg32OmUcww7on3RYdg4Va+PmSTsz/K68vbdEjh4u" crossorigin="anonymous" -->
    <link rel="apple-touch-icon" href="/bootstrap/img/apple-touch-icon.png">
    <link rel="apple-touch-icon" sizes="72x72" href="/bootstrap/img/apple-touch-icon-72x72.png">
    <link rel="apple-touch-icon" sizes="114x114" href="/bootstrap/img/apple-touch-icon-114x114.png">

<!-- jQuery (necessary for plugins) -->
<!-- <script src="https://ajax.googleapis.com/ajax/libs/jquery/1.12.4/jquery.min.js"></script> -->
<script type="text/javascript" src="js/jquery/src/minified/jquery-3.2.1.min.js"></script>

<!--- The following scripts are necessary to do TweenMax tweens, includes CSSpack properties -->
<script type="text/javascript" src="js/gsap/src/minified/TweenMax.min.js"></script>
<script type="text/javascript" src="js/gsap/src/minified/TimelineMax.min.js"></script>

<script src="./images/effectsData.js"></script>

<!--
One way to explode items at: https://greensock.com/forums/topic/7622-one-way-to-explode-items-example-included/
                        and: https://codepen.io/netgfx/pen/FpiJw?editors=1111

Posted April 28, 2013
This is an example that I tailored that uses GSAP to imitate exploding objects.
It uses multiple canvases on one element but without the need to re-draw them.
I understand this might not be the best solution for large objects but it works
nicely with small objects and it is easy to integrate.
-->

<style type="text/css">
  .buttons a {
      padding: 0 6px;
      text-decoration: underline;
      color: blue;
      cursor: pointer
  }
  .buttons a:hover {
      color: green;
  }
  .containerDiv {
    width: 100%;
    height: 100%;
    background-color: red;
    border: 2px solid black;
  }
</style>
</head>

<body>

  <div class="buttons">
    <a id="convert" style="margin-left: 680px;">CONVERT</a>
    <a id="explode" style="margin-left: 10px;">EXPLODE!</a>
    <a id="collaspe" style="margin-left: 10px;">COLLASPE!</a>
    <a id="reset" style="margin-left: 10px;">RESET</a>
  </div>

  <div id="containerDiv" class="containerDiv">
    <div class="canvas-col" style="display: inline-block;">
  		<img id="selectedPhoto" photoType="color" photoTag="mike"
  				 src="./images/mike_stern_422x436.jpg" data-src=""
      />
  </div>

<script type="text/javascript">

//------------------------------------------------------------------------------
$( document ).ready( function() {
  //----------------------------------------------------------------------------
  console.log( "1) $( document ).ready()");
  // Create plugIn instance, defaults.
  var trrPlugin = new TrrEffect();
  // Select, display default photo.
  trrPlugin.newPhoto( { photoType: "color", photoTag: "meg", imgSrc: './images/meg_CC_422x436.jpg' },
  /*1-Resume here when done*/ function( img ) {
  // Add click handlers for various functions.
  $( "#convert" ).click( function() {
    trrPlugin.convert();
  });
  $( "#explode" ).click( function() {
    trrPlugin.explode();
  });
  $( "#collaspe" ).click( function() {
    trrPlugin.collaspe();
  });
  $( "#reset" ).click( function() {
    trrPlugin.reset();
  });
  /*1-*/}.bind( this ));
}); //end $( document ).ready()


// plugIn class in context of instance, i.e. this or TrrEffect.xxxx
//------------------------------------------------------------------------------
function TrrEffect() {
  //----------------------------------------------------------------------------
  console.log( "2) TrrEffect() Create new TrrEffect instance. *");
  // Public CONSTANTS accessible via TrrEffect.xxx
  var TAU = Math.PI * 2;
  var ROOT_2 = Math.sqrt(2);
  var $el = $( '#selectedPhoto' );

  this.$el = $el;
  this.defaults = updateSettings( {
        img: document.getElementById( 'selectedPhoto'),
        $img: $el,
        photoTag: $el.attr('photoTag'),
        photoType: $el.attr('photoType'), } );
  var timeNow = new Date().getTime();
	this.id = 'mapTrrEffect_' + timeNow;
	this.particles = [];

  // Public methods accessible via instance. or this.xxxx
  //----------------------------------------------------------------------------
  this.newPhoto = function( options, /*Code to resume when done*/ callback ) {
    //--------------------------------------------------------------------------
    //this.settings = updateSettings( options );
    callback();
    //console.log( "3) newPhoto() photoType: '" + this.settings.photoType +
    //             "'. photoTag: '" + this.settings.photoTag +
    //             "'. Current img.src: '" + this.settings.img.src +
    //             "'. New imgSrc: '" + this.settings.imgSrc + "'. *");
    var src = this.settings.imgSrc,
        img = this.settings.img,
        $img = this.settings.$img;

    img.onload =
    /*1-Resume here when done*/ function() {
    console.log( " ..*3a) newPhoto() img.onload() Loaded src: '" + $img.attr('src') +
                 "'. img.width: '" + img.width + "'. img.height: '" + img.height +
                 "'. *");
    callback( img );
    /*1-*/}.bind( this ); // end img.onload function()

    $img.attr('src', src); // causes photo to be loaded and rendered.
  } // end: this.newPhoto function()

  // Private methods in context of plugIn instance, i.e. this
  //----------------------------------------------------------------------------
  function updateSettings( options ) {
    //--------------------------------------------------------------------------
    var merged = $.extend( {}, this.defaults, options );
    return merged;
  }
}; // end function TrrEffect()

// Static methods in context of window
//------------------------------------------------------------------------------
function getRandom( max, min ) {
  //----------------------------------------------------------------------------
  return Math.floor( Math.random() * ( 1 + max - min ) + min );
} // end function getRandom()

</script>

</body>

</html>

<!-- PREVIOUS EXAMPLES ========================= -->

<!--

<body>

<center style="margin-top: 80px;">
<img id="photo" src="https://mdn.mozillademos.org/files/5397/rhino.jpg">
</center>

<script type="text/javascript">

  var element = $("#photo");

  // Sequencing and grouping tweens with TimelineLite

  // Unlike most other JS animation tools, sequencing in GSAP is much more
  // flexible than building a queue of tweens that run one-after-the-other.
  // You have complete control over the relative timing of each tween - they
  // can overlap as much as you want. And you can control entire sequences as
  // a whole, reverse smoothly anytime, jump to any point, adjust the timeScale,
  // etc. and everything renders in the proper order. Watch this video for a
  // visual demo showing how TimelineLite can save you a lot of time. Of course
  // you could sequence tweens by using the "delay" special property on all your
  // tweens, but that can get complicated when you build a long sequence and
  // then later want to change the timing of something early in the sequence
  // (you'd have to adjust all the delay values in tweens after that). Plus it
  // would be a pain to control the whole sequence, like to pause() or resume()
  // or reverse() the group on-the-fly. Sequencing is much easier with
  // TimelineLite and its big brother, TimelineMax.

  // Let's jump into some sample code:

  //create a TimelineLite instance
  var tl = new TimelineMax();

  //append a to() tween
  tl.to(element, 1, { width: "50%" });

  //add another sequenced tween (by default, tweens are added to the end of the
  //timeline which makes sequencing simple)
  tl.to(element, 1, { height: "300px", ease:Elastic.easeOut });

  //offset the next tween by 0.75 seconds so there's a gap between the end of the previous tween and this new one
  tl.to(element, 1, {opacity:0.5}, "+=0.75");

  t1.to(element, 2, {rotation:"-170_short"}, "+=0.75");

  //overlap the next tween with the previous one by 0.5 seconds (notice the negative offset at the end)
  tl.to(element, 1, {backgroundColor:"#FF0000"}, "-=0.5");

  //animate 3 elements (e1, e2, and e3) to a rotation of 60 degrees, and stagger their start times by 0.2 seconds
  //tl.staggerTo([e1, e2, e3], 1, {rotation:60}, 0.2);

  //then call myFunction()
  tl.call(myFunction);

    //reverse (always goes back towards the beginning)
  //  setTimeout( function() {
  //    tween.reverse();
  //  }, 7000);

  //now we can control the entire sequence with the standard methods like these:
  //tl.pause();
  //tl.resume();
  //tl.restart();
  //tl.reverse();
  //tl.play();

  //jump to exactly 2.5 seconds into the animation
  //tl.seek(2.5);

  //slow down playback to 10% of the normal speed
  //tl.timeScale(0.1);

  //add a label named "myLabel" at exactly 3 seconds:
  //tl.add("myLabel", 3);

  //add a tween that starts at "myLabel"
  //tl.add( TweenLite.to(element, 1, {scale:0.5}), "myLabel");

  //jump to "myLabel" and play from there:
  //tl.play("myLabel");

  // Think of a timeline (as in a TimelineLite or TimelineMax instance) like a
  // collection of tweens that are positioned at specific places on that
  // timeline. It controls their playback. Timelines can be nested inside other
  // timelines as deeply as you want. This is a very powerful concept because
  // it allows you to control entire sequences in a modular way. Imagine 100
  // characters individually animating into place in a staggered fashion
  // (100 tweens). They could all be grouped into a TimelineLite instance and
  // then controlled as a whole (using common methods like pause(), resume(),
  // reverse(), restart(), etc.). In fact, you could create functions that
  // return animations wrapped in a TimelineLite so that you can easily build
  // a larger, more complex animation in a modular way. A central concept to
  // grasp is that every tween is inserted into a timeline. By default, it's
  // the root timeline inside the engine. When a timeline is playing, its
  // virtual playhead advances. If you reverse() a timeline, the playhead
  // travels in the opposite direction back towards its beginning. As the
  // timeline's playhead encounters tweens, it plays them accordingly.
  // For example, if the playhead is positioned halfway through a tween, that
  // tween will render as though it is 50% finished. If the timeline's
  // timeScale is set to 0.5, that would cause the playhead to travel at half
  // speed. Consequently, any tweens it encounters would also appear to progress
  // at half speed. Once you get the hang of how timelines work, they can
  // revolutionize your animation workflow. Just like tweens, timelines play
  // immediately by default but you can pause them initially using pause() or
  // by setting paused:true in the vars parameter of the constructor. There are
  // quite a few methods available in the timeline classes that give you precise
  // control, and we'd encourage you to look through the TimelineLite
  // Documentation to see what's available. If you can think of something you'd
  // like to do, chances are there's a way to do it.

</script>

</body>
-->

<!--
<body>

<center style="margin-top: 200px;">
<img id="photo" src="https://mdn.mozillademos.org/files/5397/rhino.jpg">
</center>

<script type="text/javascript">

  var element = $("#photo");

  // Controlling tweens

  // Most other animation tools offer very limited controls, but GSAP was built
  // from the ground up to be a professional-grade robust set of animation
  // tools. You can easily pause(), resume() reverse(), restart(), seek(), or
  // even alter the timeScale of any tween. In fact, you can tween the timeScale
  // of another tween to gradually slow it down or speed it up. To control a
  // tween, however, you need an instance to work with. The to(), from(), and
  // fromTo() methods all return an instance, so you can dump it into a variable
  // as easily as:

  //using the static to() method...
  //var tween = TweenLite.to(element, 1, {width:"50%"});

  //or use the object-oriented syntax...
  var tween = new TweenLite(element, 5, {width:"50%"});

  // Then, you can call any of its methods:

  //pause
  //tween.pause();

  //resume (honors direction - reversed or not)
  //tween.resume();

  //reverse (always goes back towards the beginning)
  setTimeout( function() {
    tween.reverse();
  }, 7000);

  //jump to exactly 0.5 seconds into the tween
  //tween.seek(0.5);

  //make the tween go half-speed
  //tween.timeScale(0.5);

  //make the tween go double-speed
  //tween.timeScale(2);

  //immediately kill the tween and make it eligible for garbage collection
  //tween.kill();

  // You can also kill ALL of the tweens of a particular element/target like this:

  // TweenLite.killTweensOf(myElement);

  // See the TweenLite Documentation for details about all of the properties
  // and methods available.

</script>

</body>
-->

<!--
<body>

<center style="margin-top: 200px;">
<img id="photo" src="https://mdn.mozillademos.org/files/5397/rhino.jpg">
</center>

<script type="text/javascript">

  var element = $("#photo");

  // directionalRotation -

  // tweens rotation in a particular direction which can
  // be either clockwise ("_cw" suffix), counter-clockwise ("_ccw" suffix), or
  // in the shortest direction ("_short" suffix) in which case the plugin
  // chooses the direction for you based on the shortest path. For example,
  // if the element's rotation is currently 170 degrees and you want to tween
  // it to -170 degrees, a normal rotation tween would travel a total of 340
  // degrees in the counter-clockwise direction, but if you use the "_short"
  // suffix, it would travel 20 degrees in the clockwise direction instead.
  // Example
  //TweenLite.to(element, 2, {rotation:"-170_short"});

  // or even use it on 3D rotations and use relative prefixes:
  //TweenLite.to(element, 2, {rotation:"-170_short", rotationX:"-=30_cw", rotationY:"1.5rad_ccw"});

  // Prior to version 1.9.0, directionalRotation was called shortRotation and it
  // only handled going in the shortest direction. The new directionalRotation
  // functionality is much more flexible and easy to use (just slap a suffix on
  // the regular property). For backwards compatibility, CSSPlugin still
  // recognizes "shortRotation", but it has been deprecated.

  // autoAlpha - the same thing as "opacity" except that when the value hits "0",
  // the "visibility" property will be set to "hidden" in order to improve
  // browser rendering performance and prevent clicks/interactivity on the
  // target. When the value is anything other than 0, "visibility" will be set
  // to "visible".
  // Example: fade out and set visibility:hidden
  //TweenLite.to(element, 5, {autoAlpha:0});
  // in 2 seconds, fade back in with visibility:visible
  //TweenLite.to(element, 10, {autoAlpha:1, delay:7});

  // className -
  // allows you to morph between classes on an element. For example, let's say
  // myElement has a class of "class1" currently and you want to change to
  // "class2" and animate the differences, you could do this:
  //TweenLite.to(myElement, 1, {className:"class2"});

  // And if you want to ADD the class to the existing one, you can simply use
  // the "+=" prefix. To remove a class, use the "-=" prefix like this:
  //TweenLite.to(myElement, 1, {className:"+=class2"});

  // Note: there are a few css-related properties that don't tween like IE
  // filters, but that is a very rare exception. Also, there is a slight speed
  // penalty when using className because the engine needs to loop through all
  // of the css properties to analyze which ones are different.

  // autoRound -
  // By default, CSSPlugin will round pixel values and zIndex to the closest
  // integer during the tween (the inbetween values) because it improves browser
  // performance, but if you'd rather disable that behavior, pass
  // autoRound:false in the css object. You can still use the RoundPropsPlugin
  // to manually define properties that you want rounded.

</script>

</body>
-->

<!--

<body>

<center style="margin-top: 200px;">
<img id="photo" src="https://mdn.mozillademos.org/files/5397/rhino.jpg">
</center>

<script type="text/javascript">

  var photo = $("#photo");
  // transformOrigin - Sets the origin around which all transforms occur.
  // By default, it is in the center of the element ("50% 50%"). You can
  // define the values using the keywords "top", "left", "right", or "bottom"
  // or you can use percentages (bottom right corner would be "100% 100%") or
  // pixels. If, for example, you want an object to spin around its top left
  // corner you can do this:

  // spins around the element's top left corner
  TweenLite.to("#photo", 2, {rotation:360, transformOrigin:"left top"});


</script>

</body>
-->

<!--
  var photo = $("#photo");
  // You can animate 3D transform properties and 2D properties (except skew)
  // together intuitively:
  TweenLite.to("#photo", 2, {rotationX:720, scaleX:1.8, z:-100});
-->

<!--
  var photo = $("#photo");
  // By default, rotation, skewX, and skewY use degrees but you can use radians
  // if you prefer. Simply append one of the standard suffixes ("rad" or "deg")
  // like this:
  //use "deg" or "rad"
  TweenLite.to(photo, 2, {rotation: "300deg", skewX:"30deg"});
-->

<!--
  var photo = $("#photo");

  //Plugins
  // Think of plugins like special properties that are dynamically added to
  // TweenLite, giving it extra abilities. This keeps the core engine small and
  // efficient, yet allows for virtually unlimited capabilities to be added
  // dynamically. Each plugin is associated with a property name and it takes
  // responsibility for handling that property. For example, the CSSPlugin is
  // associated with the "css" property name so if it loaded, it will intercept
  // the "css" property, and the ScrollToPlugin will intercept the "scrollTo"
  // value, etc.:

  //CSSPlugin will intercept the "css" value...
  TweenLite.to(photo, 1, {css:{scaleX:0.5, rotation:30}, ease:Power3.easeOut});

  //ScrollToPlugin will intercept the "scrollTo" value (if it's loaded)...
  TweenLite.to(window, 2, {scrollTo:{y:300}, ease:Bounce.easeOut});
-->

<!--
  var photo = $("#photo");

// To get linear motion, just use the Linear.easeNone ease.
TweenLite.to(photo, 1, {width:100, ease:"Linear.easeNone"});
TweenLite.to(photo, 1, {height:200, ease:"Linear.easeNone"});
-->

<!--

  var photo = $("#photo");

  // The default ease in TweenLite is Power1.easeOut (which gives a more natural
  // feel than a linear ease). Here is the syntax for defining the ease for a
  // few tweens:
  TweenLite.to(photo, 1, {width:100, ease:Power2.easeOut});
  TweenLite.to(photo, 1, {height:200, ease:Elastic.easeOut});
-->

<!--
Let's say, for example, you have an <img> with an id of "photo" and you'd like
to tween its "width" property to a value of 100 over the course of 1.5 seconds.
You can use TweenLite's to() method:

<style type="text/css">

</style>
</head>

<body>

<img id="photo" src="https://mdn.mozillademos.org/files/5397/rhino.jpg">

<script type="text/javascript">

  var photo = $("#photo");

  //notice there's no "()" after the onComplete function because it's just a reference to the function itself (you don't want to call it yet)
  TweenLite.to(photo, 1.5, {width:100, delay:0.5, onComplete:myFunction});
  function myFunction() {
      console.log("tween finished");
  }

</script>

</body>
-->

<!--
The logo element will now have its css "left" property tweened to 632px over the course of 1 second. The syntax is:
TweenLite.to( [target object], [duration in seconds], [destination values] )
-->
<!--
<style type="text/css">
    body{
      background-color:#000;
      color:white;
    }
    #demo {
      width: 692px;
      height: 60px;
      background-color: #333;
      padding: 8px;
    }
    #logo {
      position: relative;
      width: 60px;
      height: 60px;
      background: url(https://s3-us-west-2.amazonaws.com/s.cdpn.io/16327/logo_black_1.jpg)no-repeat;
    }
</style>
</head>

<body>

<div id="demo">
    <div id="logo"></div>
</div>


<script type="text/javascript">
//we'll use a window.onload for simplicity, but typically it is best to use either jQuery's $(document).ready() or $(window).load() or cross-browser event listeners so that you're not limited to one.
window.onload = function(){
    var logo = document.getElementById("logo");
    TweenLite.to(logo, 1, {left:"632px"});
}
</script>

</body>
-->
===================
