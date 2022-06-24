<script lang="ts">
    import logo from "./assets/svelte.png";
    import template from "./assets/template.jpg";
    import Counter from "./lib/Counter.svelte";
    import Footer from "./lib/Footer.svelte";
    import { saveAs } from "file-saver";
    import domtoimage from "dom-to-image";
    import { copyImageToClipboard } from "copy-image-clipboard";

    type CampusHighlight =
        | "bangkhen"
        | "kampangsan"
        | "sriracha"
        | "suphanburi"
        | "sakhonakhon"
        | "";

    type StatusHighlight = "single" | "taken" | "";

    type LearnHighlight = "onsite" | "online" | "";

    type AccommodationHighlight = "dormitory" | "condo" | "home" | "";

    type TargetHighlight = "straightA" | "party" | "";

    enum positionCampus {
        bangkhen = "top-[425px] h-[30px] w-[8rem] left-[20px]",
        kampangsan = "top-[425px] h-[30px] w-[10rem] left-[162px]",
        sriracha = "top-[425px] h-[30px] w-[8rem] left-[327px]",
        suphanburi = "top-[453px] h-[30px] w-[9rem] left-[35px]",
        sakhonakhon = "top-[453px] h-[30px] w-[11rem] left-[11.5rem]",
    }

    enum status {
        single = "top-[507px] h-[30px] w-[5rem] left-[115px]",
        taken = "top-[507px] h-[30px] w-[6rem] left-[1rem]",
    }

    let campusHighlight: CampusHighlight = "";

    let statusHighlight: StatusHighlight = "";

    let accommodationHighlight: AccommodationHighlight = "";

    let learnHighlight: LearnHighlight = "";

    let targetHighlight: TargetHighlight = "";

    let files: FileList | null = null;

    let isHide = true;

    let area;

    let saving: boolean = false;
    let isCopy: boolean = false;

    function downloadImage() {
        domtoimage
            .toPng(area)
            .then(function (blob) {
                saveAs(blob, `ku-stats.png`);
            })
            .catch(function (error) {
                console.error("oops, something went wrong!", error);
            });
    }
    function copyImage() {
        saving = true;
        domtoimage
            .toPng(area)
            .then(function (dataUrl) {
                let img = new Image();
                img.src = dataUrl;
                copyImageToClipboard(img.src);
                saving = false;
            })
            .catch(function (error) {
                console.error("oops, something went wrong!", error);
            });
        isCopy = !isCopy;
        setTimeout(() => {
            isCopy = !isCopy;
        }, 5000);
    }
</script>

<div class="font-extrabold text-3xl flex justify-center mt-5 bg-clip-text text-transparent bg-gradient-to-r from-pink-500 to-violet-500">KU Stats</div>

<div
    class="flex flex-col items-center p-2 gap-3 scale-[0.6] sm:scale-75 md:scale-90 lg:scale-100"
>
    <div class="flex flex-col items-center">
        <div class="p-10 font-bold text-xl">
            <div
                bind:this={area}
                class="w-[480px] h-[853px] border-2 flex flex-col gap-5 items-center bg-image relative "
            >
                {#if files}
                    <div
                        class="absolute  text-white flex justify-center items-center top-[13.8rem] left-[1.8rem] z-10 border-2 bg w-[11.5rem] h-[11.5rem] bg-green-500 hover:bg-green-600"
                    >
                        <img
                            class="w-[11.5rem] h-[11.5rem] object-cover"
                            src={URL.createObjectURL(files[0])}
                            alt="profile"
                        />
                    </div>
                {/if}

                <input
                    class={`absolute top-[148px] w-[11rem] right-[45px] bg-transparent ${
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
                    on:click={() => (campusHighlight = "bangkhen")}
                    class={`absolute hover:bg-green-400/30 z-10 ${positionCampus.bangkhen} ${
                        campusHighlight === "bangkhen" ? "bg-yellow-200/50" : ""
                    } rounded-xl`}
                />

                <div
                    on:click={() => (campusHighlight = "kampangsan")}
                    class={`absolute hover:bg-green-400/30 z-10 ${positionCampus.kampangsan} ${
                        campusHighlight === "kampangsan"
                            ? "bg-yellow-200/50"
                            : ""
                    } rounded-xl`}
                />

                <div
                    on:click={() => (campusHighlight = "sakhonakhon")}
                    class={`absolute hover:bg-green-400/30 z-10 ${positionCampus.sakhonakhon} ${
                        campusHighlight === "sakhonakhon"
                            ? "bg-yellow-200/50"
                            : ""
                    } rounded-xl`}
                />

                <div
                    on:click={() => (campusHighlight = "sriracha")}
                    class={`absolute hover:bg-green-400/30 z-10 ${positionCampus.sriracha} ${
                        campusHighlight === "sriracha" ? "bg-yellow-200/50" : ""
                    } rounded-xl`}
                />

                <div
                    on:click={() => (campusHighlight = "suphanburi")}
                    class={`absolute hover:bg-green-400/30 z-10 ${positionCampus.suphanburi} ${
                        campusHighlight === "suphanburi"
                            ? "bg-yellow-200/50"
                            : ""
                    } rounded-xl`}
                />

                <div
                    on:click={() => (statusHighlight = "taken")}
                    class={`absolute hover:bg-green-400/30 z-10 ${status.taken} ${
                        statusHighlight === "taken" ? "bg-yellow-200/50" : ""
                    } rounded-xl`}
                />
                <div
                    on:click={() => (statusHighlight = "single")}
                    class={`absolute hover:bg-green-400/30 z-10 ${status.single} ${
                        statusHighlight === "single" ? "bg-yellow-200/50" : ""
                    } rounded-xl`}
                />
                <div
                    on:click={() => (accommodationHighlight = "dormitory")}
                    class={`absolute hover:bg-green-400/30 z-10 top-[35rem] h-[30px] w-[9rem] left-[1rem] ${
                        accommodationHighlight === "dormitory"
                            ? "bg-yellow-200/50"
                            : ""
                    } rounded-xl`}
                />
                <div
                    on:click={() => (accommodationHighlight = "condo")}
                    class={`absolute hover:bg-green-400/30 z-10 top-[35rem] h-[30px] w-[6rem] left-[10.5rem] ${
                        accommodationHighlight === "condo"
                            ? "bg-yellow-200/50"
                            : ""
                    } rounded-xl`}
                />
                <div
                    on:click={() => (accommodationHighlight = "home")}
                    class={`absolute hover:bg-green-400/30 z-10 top-[35rem] h-[30px] w-[6rem] left-[16.5rem] ${
                        accommodationHighlight === "home"
                            ? "bg-yellow-200/50"
                            : ""
                    } rounded-xl`}
                />
                <div
                    on:click={() => (learnHighlight = "online")}
                    class={`absolute hover:bg-green-400/30 z-10 top-[617px] h-[30px] w-[6rem] left-[1rem] ${
                        learnHighlight === "online" ? "bg-yellow-200/50" : ""
                    } rounded-xl`}
                />
                <div
                    on:click={() => (learnHighlight = "onsite")}
                    class={`absolute hover:bg-green-400/30 z-10 top-[617px] h-[30px] w-[6rem] left-[7.5rem] ${
                        learnHighlight === "onsite" ? "bg-yellow-200/50" : ""
                    } rounded-xl`}
                />

                <div
                    on:click={() => (targetHighlight = "straightA")}
                    class={`absolute hover:bg-green-400/30 z-10 top-[671px] h-[30px] w-[8rem] left-[1.5rem] ${
                        targetHighlight === "straightA"
                            ? "bg-yellow-200/50"
                            : ""
                    } rounded-xl`}
                />
                <div
                    on:click={() => (targetHighlight = "party")}
                    class={`absolute hover:bg-green-400/30 z-10 top-[671px] h-[30px] w-[6rem] left-[9rem] ${
                        targetHighlight === "party" ? "bg-yellow-200/50" : ""
                    } rounded-xl`}
                />
            </div>
            <div class="flex flex-col gap-2 mt-3">
                <div class="flex flex-col gap-2 mt-3">
                    <div>อัพโหลดรูปภาพ</div>
                    <input bind:files type="file" />
                </div>
                <div class="flex flex-col gap-2 mt-3">
                    <div
                        on:click={() => downloadImage()}
                        class="bg-green-700 hover:bg-green-800 px-3 py-2 rounded-xl flex justify-center cursor-pointer select-none text-white font-bold"
                    >
                        Download
                    </div>
                    <div
                        on:click={() => copyImage()}
                        class="bg-green-700 hover:bg-green-800 px-3 py-2 rounded-xl flex justify-center cursor-pointer select-none text-white font-bold"
                    >
                        {isCopy ? "Copied" : "Copy"}
                    </div>
                </div>
            </div>
        </div>
    </div>
</div>
<Footer />

<style>
    .bg-image {
        background-image: url("/template.jpg");
    }
</style>
