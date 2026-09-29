<script lang="ts">
  type Category = 'Shorts' | 'AI comedy' | 'Animation' | 'Odd news';
  type Clip = { title: string; creator: string; category: Category; duration: string; caption: string; art: string; featured?: boolean };

  const clips: Clip[] = [
    { title: 'Local Pigeon Elected Mayor', creator: 'Bird Law Studios', category: 'AI comedy', duration: '0:42', caption: 'A landslide victory', art: 'poster-one', featured: true },
    { title: 'The Last Brain Cell at 2 AM', creator: 'Sleepy Llama', category: 'Shorts', duration: '0:58', caption: 'One thought. No plan.', art: 'poster-two' },
    { title: 'Grandma Joins a Boy Band', creator: 'Pixel Picnic', category: 'Animation', duration: '1:12', caption: 'Tour starts Tuesday', art: 'poster-three' },
    { title: 'Tiny Horse, Huge Confidence', creator: 'Good Egg Films', category: 'AI comedy', duration: '0:36', caption: 'Big hoof energy', art: 'poster-four' },
    { title: 'Breaking: Clouds Are Just Sheep', creator: 'The Almost News', category: 'Odd news', duration: '1:04', caption: 'Experts are baffled', art: 'poster-five' },
    { title: 'A Very Serious Dance Tutorial', creator: 'Mossy Media', category: 'Animation', duration: '0:49', caption: 'Please stretch first', art: 'poster-six' },
  ];

  const categories = ['All clips', 'AI comedy', 'Shorts', 'Animation', 'Odd news'] as const;
  let activeCategory = $state<string>('All clips');
  let query = $state('');
  let isLight = $state(false);
  let submitOpen = $state(false);
  let selectedClip = $state<Clip | null>(null);
  let submitted = $state(false);

  let filtered = $derived(clips.filter((clip) => {
    const matchesCategory = activeCategory === 'All clips' || clip.category === activeCategory;
    const matchesQuery = `${clip.title} ${clip.creator} ${clip.category}`.toLowerCase().includes(query.trim().toLowerCase());
    return matchesCategory && matchesQuery;
  }));

  function handleSubmit(event: SubmitEvent) {
    event.preventDefault();
    submitted = true;
    (event.currentTarget as HTMLFormElement).reset();
  }
</script>

<svelte:head><title>Oddly — clips from another timeline</title></svelte:head>
<svelte:window onkeydown={(event) => { if (event.key === 'Escape') { submitOpen = false; selectedClip = null; } }} />

<div class:light={isLight}>
  <header class="topbar">
    <a class="brand" href="#top" aria-label="Oddly home"><span class="brand-mark">o</span>oddly<span class="brand-period">.</span></a>
    <nav class="main-nav" aria-label="Main navigation"><a class="active" href="#discover">Explore</a><a href="#about">About</a><a href="#submit">Submit</a></nav>
    <div class="top-actions"><button class="icon-button" onclick={() => isLight = !isLight} aria-label="Toggle color theme" title="Toggle theme">◐</button><button class="button button-light" onclick={() => submitOpen = true}>＋ <span>Submit a clip</span></button></div>
  </header>

  <main id="top">
    <section class="hero" id="about">
      <div class="hero-copy"><span class="eyebrow"><i></i> SHORT CLIPS FROM ANOTHER TIMELINE</span><h1>Reality called.<br><span>We sent AI.</span></h1><p>A tiny home for big nonsense. Strange little stories, AI-made laughs, and clips from creators with excellent imaginations.</p><a class="button button-accent" href="#discover">Find something odd <span>↓</span></a><div class="trust-note"><span class="trust-icon">✳</span> AI-made clips are labeled. Human-made weirdness welcome.</div></div>
      <div class="hero-art" aria-label="Abstract sunset artwork"><div class="art-orbit orbit-one"></div><div class="art-orbit orbit-two"></div><div class="art-sun"></div><div class="art-hill hill-back"></div><div class="art-hill hill-front"></div><div class="art-grain"></div><div class="art-label">ODDLY SPECIFIC<br>VERY UNREAL <span>№ 001</span></div><div class="hero-sticker">100%<br>UNSERIOUS</div></div>
      <div class="hero-index">A1 <span>—</span> LOL</div>
    </section>

    <section class="collection section-wrap" id="discover">
      <div class="section-heading"><div><span class="eyebrow muted">THE CLIP-PILE</span><h2>Scroll into the <em>strange.</em></h2></div><div class="collection-meta"><span class="live-dot"></span><span>{filtered.length} clips</span><span class="meta-divider"></span><span>Freshly imagined</span></div></div>
      <div class="toolbar"><div class="filters" role="group" aria-label="Filter by category">{#each categories as category}<button class="chip" class:selected={activeCategory === category} onclick={() => activeCategory = category}>{category}</button>{/each}</div><label class="search"><span aria-hidden="true">⌕</span><input bind:value={query} type="search" placeholder="Search clips or creators" aria-label="Search clips or creators"><kbd>⌘ K</kbd></label></div>
      <div class="video-grid">
        {#each filtered as clip (clip.title)}
          <button class="film-card" onclick={() => selectedClip = clip} aria-label="Open {clip.title}">
            <div class="poster"><div class="poster-art {clip.art}" aria-hidden="true"></div><span class="film-label">{clip.caption}</span><span class="play-button" aria-hidden="true">▶</span><span class="duration">{clip.duration}</span>{#if clip.featured}<span class="ai-badge">✳ AI MADE</span>{/if}</div>
            <div class="film-info"><div><h3>{clip.title}</h3><span class="film-creator">By {clip.creator}</span></div><span class="film-category">{clip.category}</span></div>
          </button>
        {/each}
      </div>
      {#if filtered.length === 0}<div class="empty-state"><div>◌</div><h3>Nothing weird here</h3><p>Try a different search or category.</p><button class="text-button" onclick={() => { query = ''; activeCategory = 'All clips'; }}>Clear filters</button></div>{/if}
      <div class="load-row"><span>YOU'VE REACHED THE END OF THE INTERNET*</span><i></i><span>*THIS CORNER OF IT</span></div>
    </section>

    <section class="submit-banner" id="submit"><div class="banner-orb"></div><div class="banner-copy"><span class="eyebrow">GOT A GLORIOUSLY ODD IDEA?</span><h2>Make a clip.<br>Make someone's day.</h2><p>Send us an original clip you made or have permission to share. We review every submission before it joins the pile.</p><button class="button button-accent" onclick={() => submitOpen = true}>Submit your masterpiece <span>↗</span></button></div><div class="banner-side"><span class="big-asterisk">✳</span><div>GOOD VIBES<br>ONLY, PLEASE.</div></div></section>
    <section class="ad-slot" aria-label="Advertisement placement"><span>SPONSOR THIS NONSENSE</span><div>A small, clearly marked spot for a brand that gets the joke.</div><small>Ad space inactive</small></section>
  </main>

  <footer class="footer"><a class="brand" href="#top"><span class="brand-mark">o</span>oddly<span class="brand-period">.</span></a><span>A little corner of the internet where the strange is welcome.</span><div><a href="#submit">Submission policy</a><a href="mailto:hello@example.com">Contact</a><span>© 2026 ODDLY</span></div></footer>
</div>

{#if submitOpen}
  <div class="modal-backdrop" role="presentation" onclick={(event) => { if (event.target === event.currentTarget) submitOpen = false; }}>
    <dialog open class="dialog" aria-labelledby="submit-title"><button class="dialog-close" onclick={() => submitOpen = false} aria-label="Close">×</button><span class="eyebrow muted">SEND US THE GOOD STUFF</span><h2 id="submit-title">Submit a clip</h2><p class="dialog-intro">Original work and properly licensed clips welcome. We review entries before publication.</p>
      <form onsubmit={handleSubmit}><label>Clip title<input name="title" required maxlength="90" placeholder="A name people will remember"></label><label>Creator name<input name="creator" required maxlength="60" placeholder="Your name or studio"></label><label>Clip URL<input name="url" type="url" required placeholder="https://…"></label><label>Category<select name="category" required><option value="">Choose a category</option><option>AI comedy</option><option>Shorts</option><option>Animation</option><option>Odd news</option></select></label><label class="consent"><input type="checkbox" required><span>I made this clip or have permission to share it. Everyone featured agreed to its publication.</span></label><button class="button button-accent submit-form-button" type="submit">Send for review <span>↗</span></button></form>
      <p class="form-note">Demo only: this form does not upload or publish video.</p>{#if submitted}<div class="form-success" role="status">Thanks! Demo submission received in this page only.</div>{/if}
    </dialog>
  </div>
{/if}

{#if selectedClip}
  <div class="modal-backdrop" role="presentation" onclick={(event) => { if (event.target === event.currentTarget) selectedClip = null; }}>
    <dialog open class="dialog clip-dialog" aria-labelledby="clip-title"><button class="dialog-close" onclick={() => selectedClip = null} aria-label="Close">×</button><div class="clip-preview"><div class="poster-art {selectedClip.art}"></div><div class="preview-message"><span>✳</span><strong>IMAGINATION IN PROGRESS</strong><small>Demo card — video preview not connected yet</small></div></div><span class="eyebrow muted">{selectedClip.category} · {selectedClip.duration}</span><h2 id="clip-title">{selectedClip.title}</h2><p class="dialog-intro">A made-up clip from <strong>{selectedClip.creator}</strong>. Connect your own authorized video feed to enable playback.</p></dialog>
  </div>
{/if}
