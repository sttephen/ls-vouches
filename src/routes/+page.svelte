<svelte:head>
    <title>LearnSpigot Vouches</title>
</svelte:head>

<script>
    import Lazy from 'svelte-lazy';
    import "../app.css";
    import { onMount } from "svelte";
    import { shuffle } from 'lodash';

    const onload = (node) => {
        console.log('on load');
    }

    let vouchData = [];

    onMount(() => {
        fetch('/vouches.json')
            .then(response => response.json())
            .then(json => {
                vouchData = shuffle(json);

                const splitIndex = Math.ceil(vouchData.length / 3);
                const column1Data = vouchData.slice(0, splitIndex);
                const column2Data = vouchData.slice(splitIndex, splitIndex * 2);
                const column3Data = vouchData.slice(splitIndex * 2);

                vouchData = [column1Data, column2Data, column3Data];
            });
    });
</script>

<body class="bg-[#161c27] w-[200vw] lg:w-[100%]">
    <div class="lg:w-[50vw] w-[100%] lg:m-auto ml-10 flex flex-col pt-20">
        <div class="flex mb-2">
            <div class="flex font-semibold text-[20px] text-[#F0BF62] font-['Poppins'] items-center border-[3px] border-[#F0BF62] rounded-[14px] px-4">
                <p>PARTNERED WITH</p>
                <img src="/logo/jetbrains.png" class="h-4 pl-2 pr-1">
                <p>JETBRAINS</p>
            </div>
            <a href="https://learnspigot.com" class="ml-auto" target="_blank">
                <img src="/logo/learnspigot.png" class="h-10">
            </a>
        </div>
        <div class="md:w-[60%]">
            <p class="font-bold text-[25px] text-white font-['Poppins']">Not convinced on buying the course?</p>
            <p class="text-[#8090ae] font-medium text-[15px] font-['Inter']">We assume you’re here because of one of two reasons. A) you’re undecided on buying the course or B) we pinged you in <a target="_blank" href="https://discord.com/channels/397526357191557121/397528827657453569" class="text-[#B3C0D8]">#news</a> to show off our cool new site. Either way, take a read of what people who own the course have to say.</p>
        </div>
        <div class="flex-col flex gap-2 md:w-[60%] mt-10">
            <p class="font-bold text-[22px] text-[#F0BF62] font-['Poppins']">Got something to add?</p>
            <p class="text-[#8090ae] font-medium text-[15px] font-['Inter']">If you want to leave a review and have it featured here, whack it in <a target="_blank" href="https://discord.com/channels/397526357191557121/925717319974535178" class="text-[#B3C0D8]">#vouches</a> or leave a review on <a target="_blank" href="https://learnspigot.com" class="text-[#B3C0D8]">Udemy</a> so we can add it in. </p>
        </div>
        <a href="https://learnspigot.com/discord" target="_blank">
            <button class="flex bg-[#2D3748] w-fit py-3 px-8 items-center gap-3 rounded-[14px] mb-20 mt-8">
                <img src="/logo/discord_light.png" class="h-5">
                <p class="font-bold text-[18px] text-[#8090AE] font-['Poppins']">JOIN THE DISCORD</p>
            </button>
        </a>
    </div>
    <div class="flex gap-5 lg:w-[50%] pb-16 lg:m-auto">
        {#each vouchData as columnData}
            <div class="flex flex-col gap-5">
                {#each columnData as vouch}
                    <Lazy offset={150} onload={onload} class="min-w-[300px]">
                        <div class="rounded-[15px] bg-[#2D3748] p-4">
                            <div class="flex items-center gap-3.5">
                                {#if vouch.icon != "null"}
                                    <img src="{vouch.icon}" class="h-10 w-10 rounded-full">
                                {:else}
                                    <img src="/image/anon.png" class="h-10 w-10 rounded-full">
                                {/if}
                                <p class="text-white font-bold text-[17px] items-center justify-center font-['Poppins']">{vouch.name}</p>
                                {#if vouch.platform === 'bbb'}
                                    <a target="_blank" href="https://builtbybit.com/threads/new-spigot-course-11-000-students-%E2%AD%90-2-500-5%E2%98%85-reviews-beginner-%E2%86%92-advanced-24-7-support-team.191001/" class="ml-auto">
                                        <img src="/logo/{vouch.platform}.svg" class="w-5 h-5">
                                    </a>
                                {:else if vouch.platform === 'discord'}
                                    <a target="_blank" href="https://learnspigot.com/discord" class="ml-auto">
                                        <img src="/logo/{vouch.platform}.svg" class="ml-auto w-5 h-5">
                                    </a>
                                {:else if vouch.platform === 'udemy'}
                                    <a target="_blank"  href="https://learnspigot.com/999sale" class="ml-auto">
                                        <img src="/logo/{vouch.platform}.svg" class="ml-auto w-5 h-5">
                                    </a>
                                {/if}
                            </div>
                            <p class="pt-3 text-[#8090AE] text-[15px] font-medium font-['Inter']">{vouch.vouch}</p>
                        </div>
                    </Lazy>
                {/each}
            </div>
        {/each}
    </div>
</body>
