<script lang="ts">
	import { onMount } from 'svelte';
  
  onMount(async () => {
    const points:any[] = [];
    let width = window?window.innerWidth:1920
    let height = window?window.innerHeight:1080
    const c  = <HTMLCanvasElement>document.getElementById("myCanvas")
    const ctx = c.getContext("2d")
    let lastCall = performance.now()
    let tresh = 30000
    let offset = Math.sqrt(tresh)+10


    function addPoint(init:boolean)
    {
      const size = 3+Math.random()*7
      let angle = Math.random()*Math.PI
      const speed = 10+Math.random()*50
      const opacity = Math.random()*0.8+0.2;
      if(init)
      {
        return {
          x : Math.random()*width,
          y : Math.random()*height,
          size : size,
          angle : Math.random()*Math.PI*2,
          speed : speed,
          opacity : opacity
        }
      }
      const fixedX = Math.random()<0.5;
      const firstOrSecond = Math.random()<0.5;

      const x = fixedX?(firstOrSecond?-offset:width+offset):Math.random()*width
      const y = ! fixedX?(firstOrSecond?-offset:height+offset):Math.random()*height

      angle += fixedX?(firstOrSecond?0:Math.PI):(firstOrSecond?Math.PI*3/2:Math.PI/2)

      return {
        x : x,
        y : y,
        size : size,
        angle : angle,
        speed : speed,
        opacity : opacity
      };
    }

    function framePoints(time:number)
    {
      points.forEach(x => {
        x.x += Math.sin(x.angle)*time/100;
        x.y += Math.cos(x.angle)*time/100;
        x.angle+=(Math.random()-0.5)/100

        if(x.x< -offset || x.y<-offset || x.x>width+offset || x.y>height+offset ){
          Object.assign(x,addPoint(false))
        }
      })
    }

    for(let i = 0;i<80;i++)
    {
      points.push(addPoint(true))
    }

    function drawPoints(time:DOMHighResTimeStamp)
    {
      const elapsed = time-lastCall;
      lastCall = performance.now();
      if(elapsed && elapsed < 100)
      {
        framePoints(elapsed)
      }
      if(c && ctx)
      {
        
        ctx.canvas.width  = window.innerWidth;
        ctx.canvas.height = window.innerHeight;
        width = window?window.innerWidth:1920
        height = window?window.innerHeight:1080
        tresh = width*height /100
        offset = Math.sqrt(tresh)+10
        points.forEach((x,i) => {
          let grd = ctx.createRadialGradient(x.x,x.y, x.size/4, x.x,x.y,x.size);
          grd.addColorStop(0, "white");
          grd.addColorStop(1, "transparent");

          // Fill with gradient
          ctx.fillStyle = grd;
          ctx.globalAlpha = x.opacity
          ctx.beginPath();
          ctx.arc(x.x, x.y, x.size, 0, 2 * Math.PI);
          ctx.fill()

          points.forEach((y,j) => {
            if(j<i)
            {
              const dist = (x.x-y.x)*(x.x-y.x) + (x.y-y.y)*(x.y-y.y)
              if(dist < tresh)
              {
                ctx.lineWidth = 1.5
                ctx.globalAlpha = 1-Math.sqrt(1-((tresh-dist)/tresh))

                
                var grad= ctx.createLinearGradient(x.x, x.y, y.x, y.y);
                grad.addColorStop(0, "rgba(255,255,255,"+x.opacity+")");
                grad.addColorStop(1, "rgba(255,255,255,"+y.opacity+")");
                ctx.strokeStyle = grad
                ctx.beginPath();
                ctx.moveTo(x.x, x.y);
                ctx.lineTo(y.x, y.y);
                ctx.stroke();
              }
            }
          })
          ctx.globalAlpha = 1;
        })
      }

      requestAnimationFrame(drawPoints)
    }

    drawPoints(lastCall);
  })

</script>

<style>
  .background 
  {
    position : fixed;
    top : 0;
    bottom : 0;
    left : 0;
    right : 0;
    background-color: #00000D;
    z-index: -1;
  }

  canvas 
  {
    width : 100%;
    height : 100%;
  }
</style>

<div class="background"><canvas id="myCanvas"/></div>