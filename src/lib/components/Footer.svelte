<script lang="ts">
    import  { type Content, isFilled } from '@prismicio/client';
	import { PrismicLink } from '@prismicio/svelte';
    import IconGithub from '~icons/fa-brands/github'
    import IconGitlab from '~icons/fa-brands/gitlab'
    import IconDiscord from '~icons/fa-brands/discord'
	import Bounded from './Bounded.svelte';

    // Use the Content.SettingsDocument type for the settings prop
    export let settings: Content.SettingsDocument;
</script>

<Bounded as="footer" class = "text-slate-600">
    <div class="container mx-auto flex mt-20 flex-col items-center justify-between gap-6 py-8 sm:flex-row">
        <div class="name flex flex-col items-center justify-center gap-x-4 gap-y-2 sm:flex-row sm:justify-self-start">
            <a href="/" class="text-l font-extrabold tracking-tighter text-slate-100 transition-color duration-150 hover:text-yellow-400">
                {settings.data.name}
            </a>
            <span class="hidden text-5xl font-extralight leading-[0] text-slate-400 sm:inline" aria-hidden="true">/</span>
            <p class="text-sm text-slate-300"></p>
            © {new Date().getFullYear()} {settings.data.name}. All rights reserved.
        </div>
        <nav class="navigation" aria-label="Footer Navigation">
            <ul class="flex items-center gap-1">
                {#each settings.data.nav_item as {link, label}, index}
                <li>
                    <PrismicLink field={link} class="block px-3 py-1 text-base font-bold text-slate-100 transistion-colors duration-150 hover:text-yellow-400">{label}</PrismicLink>
                </li>
                {#if index < settings.data.nav_item.length - 1}
                    <span class="text-4xl font-thin leading-[0]0 text-slate-400" aria-hidden="true">
                        /
                    </span>
                {/if}
                {/each}
            </ul>
        </nav>
        <div class="socials inline-flex justify-center sm-justify-end">
            {#if isFilled.link(settings.data.github_link)}
            <PrismicLink 
                field={settings.data.github_link} 
                class="p-2 text-2xl text-slate-300 
                        transform transition-all duration-150 
                        hover:scale-125 hover:text-yellow-400"
                aria-label={settings.data.name + ' on Github'}
            >
                <IconGithub />
            </PrismicLink>
            {/if}
            {#if isFilled.link(settings.data.github_link)}
            <PrismicLink 
                field={settings.data.github_link} 
                class="p-2 text-2xl text-slate-300 
                        transform transition-all duration-150 
                        hover:scale-125 hover:text-yellow-400"
                aria-label={settings.data.name + ' on Github'}
            >
                <IconGitlab />
            </PrismicLink>
            {/if}
            {#if isFilled.link(settings.data.github_link)}
            <PrismicLink 
                field={settings.data.github_link} 
                class="p-2 text-2xl text-slate-300 
                        transform transition-all duration-150 
                        hover:scale-125 hover:text-yellow-400"
                aria-label={settings.data.name + ' on Github'}
            >
                <IconDiscord />
            </PrismicLink>
            {/if}
        </div>
    </div>
</Bounded>