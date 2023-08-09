<template>


</template>

<script>
    import GUI from 'lil-gui'
    import { Renderer, Program, Color, Mesh, Triangle } from 'ogl'
    import vertex from '../glsl/main.vert'
    import fragment from '../glsl/main.frag'

    export default {
    mounted() {
        this.setGUI()
        this.setScene()
        this.events()
    },
    methods: {
        setGUI() {
        const gui = new GUI()

        const handleChange = (value) => {
            this.program.uniforms.uOffset.value = value
        }

        gui.add(this.guiObj, 'offset', 0.5, 4).onChange(handleChange)
        },
        setScene() {
        const canvasEl = this.$el.querySelector('.scene')
        this.renderer = new Renderer({ dpr: Math.min(window.devicePixelRatio, 2), canvas: canvasEl })
        const gl = this.renderer.gl
        gl.clearColor(1, 1, 1, 1)

        this.handleResize()

        const geometry = new Triangle(gl)

        this.program = new Program(gl, {
            vertex,
            fragment,
            uniforms: {
            uTime: { value: 0 },
            uColor: { value: new Color(0.3, 0.2, 0.5) },
            uOffset: { value: this.guiObj.offset },
            },
        })

        this.mesh = new Mesh(gl, { geometry, program: this.program })
        },
        events() {
        window.addEventListener('resize', this.handleResize, false)
        requestAnimationFrame(this.handleRAF)
        },
        handleResize() {
        this.renderer.setSize(window.innerWidth, window.innerHeight)
        },
        handleRAF(t) {
        requestAnimationFrame(this.handleRAF)

        this.program.uniforms.uTime.value = t * 0.001

        this.renderer.render({ scene: this.mesh })
        },
    },
    data() {
        return {
        guiObj: {
            offset: 1,
        },
        renderer: null,
        mesh: null,
        program: null,
        }
    },
    }
</script>