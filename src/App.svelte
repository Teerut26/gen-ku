<script lang="ts">
    import logo from "./assets/svelte.png";
    import template from "./assets/template.jpg";
    import Counter from "./lib/Counter.svelte";

    type Highlight =
        | "bangkhen"
        | "kampangsan"
        | "sriracha"
        | "suphanburi"
        | "sakhonakhon";

    enum positionCampus {
        bangkhen = "top-[425px] h-[30px] w-[8rem] left-[20px]",
        kampangsan = "top-[425px] h-[30px] w-[10rem] left-[162px]",
        sriracha = "top-[425px] h-[30px] w-[8rem] left-[327px]",
        suphanburi = "top-[453px] h-[30px] w-[9rem] left-[35px]",
        sakhonakhon = "top-[453px] h-[30px] w-[11rem] left-[11.5rem]",
    }

    let campusHighlight: Highlight = "bangkhen";

    let isHide = true;
</script>

<div
    class="flex flex-col items-center p-2 gap-3 scale-[0.6] sm:scale-75 md:scale-90 lg:scale-100"
>
    <div class="flex flex-col items-center">
        <div class="p-10 bg-white ">
            <div
                class="w-[480px] h-[853px] border-2 flex flex-col gap-5 items-center bg-image relative"
            >
                <input
                    class={`absolute top-[149px] right-[41px] bg-transparent ${
                        !isHide
                            ? "border-2 border-purple-500"
                            : "focus:outline-none"
                    }`}
                    type="text"
                />
                <input
                    class={`absolute top-[250px] w-[6rem] right-[14px] bg-transparent ${
                        !isHide
                            ? "border-2 border-purple-500"
                            : "focus:outline-none"
                    }`}
                    type="text"
                />
                <input
                    class={`absolute top-[281px] w-[8rem] right-[30px] bg-transparent ${
                        !isHide
                            ? "border-2 border-purple-500"
                            : "focus:outline-none"
                    }`}
                    type="text"
                />
                <input
                    class={`absolute top-[306px] w-[8rem] right-[29px] bg-transparent ${
                        !isHide
                            ? "border-2 border-purple-500"
                            : "focus:outline-none"
                    }`}
                    type="text"
                />
                <input
                    class={`absolute top-[337px] w-[8rem] right-[43px] bg-transparent ${
                        !isHide
                            ? "border-2 border-purple-500"
                            : "focus:outline-none"
                    }`}
                    type="text"
                />
                <input
                    class={`absolute top-[363px] w-[10rem] right-[36px] bg-transparent ${
                        !isHide
                            ? "border-2 border-purple-500"
                            : "focus:outline-none"
                    }`}
                    type="text"
                />

                <div
                    on:click={() => campusHighlight = "bangkhen"}
                    class={`absolute z-10 ${positionCampus.bangkhen} ${
                        campusHighlight === "bangkhen" ? "bg-yellow-200/50" : ""
                    } rounded-xl`}
                />

                <div
                    on:click={() => campusHighlight = "kampangsan"}
                    class={`absolute z-10 ${positionCampus.kampangsan} ${
                        campusHighlight === "kampangsan"
                            ? "bg-yellow-200/50"
                            : ""
                    } rounded-xl`}
                />

                <div
                    on:click={() => campusHighlight = "sakhonakhon"}
                    class={`absolute z-10 ${positionCampus.sakhonakhon} ${
                        campusHighlight === "sakhonakhon"
                            ? "bg-yellow-200/50"
                            : ""
                    } rounded-xl`}
                />

                <div
                    on:click={() => campusHighlight = "sriracha"}
                    class={`absolute z-10 ${positionCampus.sriracha} ${
                        campusHighlight === "sriracha" ? "bg-yellow-200/50" : ""
                    } rounded-xl`}
                />

                <div
                    on:click={() => campusHighlight = "suphanburi"}
                    class={`absolute z-10 ${positionCampus.suphanburi} ${
                        campusHighlight === "suphanburi"
                            ? "bg-yellow-200/50"
                            : ""
                    } rounded-xl`}
                />
            </div>
        </div>
    </div>
</div>

<style>
    .bg-image {
        background-image: url("/template.jpg");
    }
    @apply {
    }
</style>
