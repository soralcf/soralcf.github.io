---
title: metronome
date: 2025-01-12 20:25:55
categories:
 - music
tags:
 - music
 - metronome
---

<div id="metronome-app">
<style>
/* 节拍器样式 */
#metronome-app * {
    margin: 0;
    padding: 0;
    box-sizing: border-box;
}

#metronome-app {
    --metro-primary: #3498db;
    --metro-accent: #e74c3c;
    --metro-bg: #f5f7fa;
    --metro-card: #ffffff;
    --metro-text: #2c3e50;
    --metro-gray-light: #ecf0f1;
    --metro-gray-medium: #95a5a6;
    --metro-radius: 12px;
    --metro-shadow: 0 2px 8px rgba(0, 0, 0, 0.08);
    --metro-shadow-hover: 0 4px 16px rgba(0, 0, 0, 0.12);
    font-family: -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto, sans-serif;
    margin: 30px 0;
}

.metronome-container {
    background: var(--metro-card);
    border-radius: var(--metro-radius);
    box-shadow: var(--metro-shadow);
    padding: 40px;
    width: 100%;
    max-width: 480px;
    margin: 0 auto;
}

.metronome-header {
    text-align: center;
    margin-bottom: 30px;
}

.metronome-title {
    font-size: 24px;
    font-weight: 600;
    color: var(--metro-text);
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 10px;
}

.metro-bpm-display {
    text-align: center;
    margin-bottom: 25px;
}

.metro-bpm-value {
    font-size: 72px;
    font-weight: 700;
    color: var(--metro-primary);
    line-height: 1;
    font-family: 'Roboto Mono', monospace;
    margin-bottom: 5px;
}

.metro-bpm-label {
    font-size: 14px;
    color: var(--metro-gray-medium);
    text-transform: uppercase;
    letter-spacing: 2px;
}

.metro-bpm-controls {
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 10px;
    margin-bottom: 20px;
}

.metro-bpm-btn {
    width: 44px;
    height: 44px;
    border: none;
    background: var(--metro-primary);
    color: white;
    font-size: 20px;
    border-radius: 8px;
    cursor: pointer;
    transition: all 0.3s ease;
    display: flex;
    align-items: center;
    justify-content: center;
}

.metro-bpm-btn:hover {
    background: #2980b9;
    transform: translateY(-2px);
}

.metro-bpm-input {
    width: 100px;
    height: 44px;
    border: 2px solid var(--metro-gray-light);
    border-radius: 8px;
    font-size: 20px;
    font-weight: 600;
    text-align: center;
    color: var(--metro-text);
    transition: all 0.3s ease;
}

.metro-bpm-input:focus {
    outline: none;
    border-color: var(--metro-primary);
}

.metro-preset-buttons {
    display: flex;
    justify-content: center;
    gap: 8px;
    margin-bottom: 20px;
    flex-wrap: wrap;
}

.metro-preset-btn {
    padding: 8px 16px;
    border: 2px solid var(--metro-gray-light);
    background: white;
    color: var(--metro-text);
    border-radius: 6px;
    font-size: 13px;
    font-weight: 500;
    cursor: pointer;
    transition: all 0.3s ease;
}

.metro-preset-btn:hover {
    border-color: var(--metro-primary);
    color: var(--metro-primary);
}

.metro-time-signature {
    text-align: center;
    margin-bottom: 25px;
}

.metro-time-sig-label {
    font-size: 13px;
    color: var(--metro-gray-medium);
    margin-bottom: 10px;
    text-transform: uppercase;
    letter-spacing: 1px;
}

.metro-time-sig-buttons {
    display: flex;
    justify-content: center;
    gap: 8px;
}

.metro-time-sig-btn {
    width: 60px;
    height: 40px;
    border: 2px solid var(--metro-gray-light);
    background: white;
    color: var(--metro-text);
    border-radius: 8px;
    font-size: 14px;
    font-weight: 600;
    cursor: pointer;
    transition: all 0.3s ease;
}

.metro-time-sig-btn:hover {
    border-color: var(--metro-primary);
    color: var(--metro-primary);
}

.metro-time-sig-btn.active {
    background: var(--metro-primary);
    color: white;
    border-color: var(--metro-primary);
}

.metro-beat-indicators {
    display: flex;
    justify-content: center;
    gap: 12px;
    margin-bottom: 25px;
    min-height: 60px;
    align-items: center;
}

.metro-beat-dot {
    width: 40px;
    height: 40px;
    border-radius: 50%;
    background: var(--metro-gray-light);
    transition: all 0.15s cubic-bezier(0.4, 0, 0.2, 1);
}

.metro-beat-dot.active {
    transform: scale(1.3);
}

.metro-beat-dot.strong-beat {
    background: var(--metro-accent);
}

.metro-beat-dot.weak-beat {
    background: var(--metro-primary);
}

.metro-play-button {
    width: 100%;
    padding: 16px;
    border: none;
    background: var(--metro-primary);
    color: white;
    font-size: 18px;
    font-weight: 600;
    border-radius: 8px;
    cursor: pointer;
    transition: all 0.3s ease;
    display: flex;
    align-items: center;
    justify-content: center;
    gap: 10px;
}

.metro-play-button:hover {
    background: #2980b9;
    transform: translateY(-2px);
    box-shadow: 0 4px 12px rgba(52, 152, 219, 0.3);
}

.metro-play-button.playing {
    background: var(--metro-accent);
}

.metro-play-button.playing:hover {
    background: #c0392b;
    box-shadow: 0 4px 12px rgba(231, 76, 60, 0.3);
}

.metro-status-tip {
    text-align: center;
    margin-top: 20px;
    padding: 12px;
    background: var(--metro-gray-light);
    border-radius: 8px;
    font-size: 13px;
    color: var(--metro-gray-medium);
}

.metro-status-tip kbd {
    display: inline-block;
    padding: 2px 6px;
    background: white;
    border: 1px solid #ddd;
    border-radius: 4px;
    font-family: monospace;
    font-size: 12px;
    margin: 0 2px;
}

@media (max-width: 480px) {
    .metronome-container {
        padding: 24px;
    }

    .metro-bpm-value {
        font-size: 56px;
    }

    .metro-bpm-controls {
        flex-wrap: wrap;
    }

    .metro-preset-buttons {
        gap: 6px;
    }

    .metro-preset-btn {
        padding: 6px 12px;
        font-size: 12px;
    }

    .metro-time-sig-buttons {
        flex-wrap: wrap;
    }

    .metro-beat-dot {
        width: 32px;
        height: 32px;
    }
}
</style>

<div class="metronome-container">
    <div class="metronome-header">
        <h1 class="metronome-title">🎵 在线节拍器</h1>
    </div>

    <div class="metro-bpm-display">
        <div class="metro-bpm-value" id="metroBpmValue">120</div>
        <div class="metro-bpm-label">BPM</div>
    </div>

    <div class="metro-bpm-controls">
        <button class="metro-bpm-btn" id="metroBpmDown">−</button>
        <input type="number" class="metro-bpm-input" id="metroBpmInput" value="120" min="40" max="208">
        <button class="metro-bpm-btn" id="metroBpmUp">+</button>
    </div>

    <div class="metro-preset-buttons">
        <button class="metro-preset-btn" data-bpm="60">60 慢板</button>
        <button class="metro-preset-btn" data-bpm="80">80 行板</button>
        <button class="metro-preset-btn" data-bpm="120">120 快板</button>
        <button class="metro-preset-btn" data-bpm="168">168 急板</button>
    </div>

    <div class="metro-time-signature">
        <div class="metro-time-sig-label">拍号</div>
        <div class="metro-time-sig-buttons">
            <button class="metro-time-sig-btn" data-beats="2">2/4</button>
            <button class="metro-time-sig-btn" data-beats="3">3/4</button>
            <button class="metro-time-sig-btn active" data-beats="4">4/4</button>
            <button class="metro-time-sig-btn" data-beats="6">6/8</button>
        </div>
    </div>

    <div class="metro-beat-indicators" id="metroBeatIndicators">
        <div class="metro-beat-dot" data-beat="1"></div>
        <div class="metro-beat-dot" data-beat="2"></div>
        <div class="metro-beat-dot" data-beat="3"></div>
        <div class="metro-beat-dot" data-beat="4"></div>
    </div>

    <button class="metro-play-button" id="metroPlayButton">
        <span id="metroPlayIcon">▶</span>
        <span id="metroPlayText">开始播放</span>
    </button>

    <div class="metro-status-tip">
        💡 提示: 按 <kbd>空格键</kbd> 可快速启停
    </div>
</div>

<script>
(function() {
    // 节拍器引擎
    class MetronomeEngine {
        constructor() {
            this.audioContext = null;
            this.nextNoteTime = 0.0;
            this.timerID = null;
            this.tempo = 120;
            this.lookahead = 25.0;
            this.scheduleAheadTime = 0.1;
            this.currentBeat = 0;
            this.beatsPerBar = 4;
            this.isPlaying = false;
        }

        initAudioContext() {
            if (!this.audioContext) {
                this.audioContext = new (window.AudioContext || window.webkitAudioContext)();
            }
            if (this.audioContext.state === 'suspended') {
                this.audioContext.resume();
            }
        }

        playBeat(isStrong, time) {
            const osc = this.audioContext.createOscillator();
            const gainNode = this.audioContext.createGain();

            osc.connect(gainNode);
            gainNode.connect(this.audioContext.destination);

            const frequency = isStrong ? 1000 : 600;
            const volume = isStrong ? 0.5 : 0.25;

            osc.frequency.value = frequency;
            gainNode.gain.setValueAtTime(volume, time);
            gainNode.gain.exponentialRampToValueAtTime(0.001, time + 0.05);

            osc.start(time);
            osc.stop(time + 0.05);
        }

        nextNote() {
            const secondsPerBeat = 60.0 / this.tempo;
            this.nextNoteTime += secondsPerBeat;

            this.currentBeat++;
            if (this.currentBeat > this.beatsPerBar) {
                this.currentBeat = 1;
            }
        }

        scheduleNote(beatNumber, time) {
            const isStrong = (beatNumber === 1);
            this.playBeat(isStrong, time);

            const drawTime = (time - this.audioContext.currentTime) * 1000;
            setTimeout(() => {
                requestAnimationFrame(() => {
                    metroUpdateVisuals(beatNumber, isStrong);
                });
            }, drawTime);
        }

        scheduler() {
            while (this.nextNoteTime < this.audioContext.currentTime + this.scheduleAheadTime) {
                this.scheduleNote(this.currentBeat, this.nextNoteTime);
                this.nextNote();
            }
            this.timerID = setTimeout(() => this.scheduler(), this.lookahead);
        }

        start() {
            if (this.isPlaying) return;
            this.initAudioContext();
            this.isPlaying = true;
            this.currentBeat = 1;
            this.nextNoteTime = this.audioContext.currentTime + 0.05;
            this.scheduler();
            metroUpdatePlayButton(true);
        }

        stop() {
            this.isPlaying = false;
            clearTimeout(this.timerID);
            metroUpdatePlayButton(false);
            metroResetVisuals();
        }

        setTempo(bpm) {
            this.tempo = Math.max(40, Math.min(208, bpm));
        }

        setBeatsPerBar(beats) {
            this.beatsPerBar = beats;
            this.currentBeat = 1;
        }

        getTempo() {
            return this.tempo;
        }
    }

    const metronome = new MetronomeEngine();
    const bpmValue = document.getElementById('metroBpmValue');
    const bpmInput = document.getElementById('metroBpmInput');
    const bpmUp = document.getElementById('metroBpmUp');
    const bpmDown = document.getElementById('metroBpmDown');
    const presetButtons = document.querySelectorAll('.metro-preset-btn');
    const timeSigButtons = document.querySelectorAll('.metro-time-sig-btn');
    const beatIndicators = document.getElementById('metroBeatIndicators');
    const playButton = document.getElementById('metroPlayButton');
    const playText = document.getElementById('metroPlayText');
    const playIcon = document.getElementById('metroPlayIcon');

    function metroUpdateBPM(bpm) {
        bpmValue.textContent = bpm;
        bpmInput.value = bpm;
        metronome.setTempo(bpm);
        metroSaveSettings();
    }

    function metroUpdateVisuals(beatNumber, isStrong) {
        const dots = document.querySelectorAll('.metro-beat-dot');
        dots.forEach(dot => {
            dot.classList.remove('active', 'strong-beat', 'weak-beat');
        });

        const activeDot = document.querySelector(`.metro-beat-dot[data-beat="${beatNumber}"]`);
        if (activeDot) {
            activeDot.classList.add('active');
            activeDot.classList.add(isStrong ? 'strong-beat' : 'weak-beat');
        }
    }

    function metroResetVisuals() {
        const dots = document.querySelectorAll('.metro-beat-dot');
        dots.forEach(dot => {
            dot.classList.remove('active', 'strong-beat', 'weak-beat');
        });
    }

    function metroUpdatePlayButton(isPlaying) {
        if (isPlaying) {
            playButton.classList.add('playing');
            playText.textContent = '暂停';
            playIcon.textContent = '⏸';
        } else {
            playButton.classList.remove('playing');
            playText.textContent = '开始播放';
            playIcon.textContent = '▶';
        }
    }

    function metroUpdateBeatIndicators(beats) {
        beatIndicators.innerHTML = '';
        for (let i = 1; i <= beats; i++) {
            const dot = document.createElement('div');
            dot.className = 'metro-beat-dot';
            dot.setAttribute('data-beat', i);
            beatIndicators.appendChild(dot);
        }
    }

    bpmInput.addEventListener('change', () => {
        let bpm = parseInt(bpmInput.value);
        bpm = Math.max(40, Math.min(208, bpm));
        metroUpdateBPM(bpm);
    });

    bpmUp.addEventListener('click', () => {
        const current = metronome.getTempo();
        metroUpdateBPM(Math.min(208, current + 1));
    });

    bpmDown.addEventListener('click', () => {
        const current = metronome.getTempo();
        metroUpdateBPM(Math.max(40, current - 1));
    });

    presetButtons.forEach(btn => {
        btn.addEventListener('click', () => {
            const bpm = parseInt(btn.getAttribute('data-bpm'));
            metroUpdateBPM(bpm);
        });
    });

    timeSigButtons.forEach(btn => {
        btn.addEventListener('click', () => {
            const beats = parseInt(btn.getAttribute('data-beats'));
            timeSigButtons.forEach(b => b.classList.remove('active'));
            btn.classList.add('active');
            metronome.setBeatsPerBar(beats);
            metroUpdateBeatIndicators(beats);
            metroSaveSettings();
        });
    });

    playButton.addEventListener('click', () => {
        if (metronome.isPlaying) {
            metronome.stop();
        } else {
            metronome.start();
        }
    });

    document.addEventListener('keydown', (e) => {
        if (e.code === 'Space') {
            e.preventDefault();
            if (metronome.isPlaying) {
                metronome.stop();
            } else {
                metronome.start();
            }
        }

        if (e.code === 'ArrowUp') {
            e.preventDefault();
            const current = metronome.getTempo();
            metroUpdateBPM(Math.min(208, current + 1));
        }

        if (e.code === 'ArrowDown') {
            e.preventDefault();
            const current = metronome.getTempo();
            metroUpdateBPM(Math.max(40, current - 1));
        }
    });

    const METRO_STORAGE_KEY = 'metronome-settings';

    function metroSaveSettings() {
        const settings = {
            bpm: metronome.getTempo(),
            beatsPerBar: metronome.beatsPerBar
        };
        localStorage.setItem(METRO_STORAGE_KEY, JSON.stringify(settings));
    }

    function metroLoadSettings() {
        const saved = localStorage.getItem(METRO_STORAGE_KEY);
        if (saved) {
            try {
                const settings = JSON.parse(saved);

                if (settings.bpm) {
                    metroUpdateBPM(settings.bpm);
                }

                if (settings.beatsPerBar) {
                    metronome.setBeatsPerBar(settings.beatsPerBar);
                    metroUpdateBeatIndicators(settings.beatsPerBar);

                    timeSigButtons.forEach(btn => {
                        btn.classList.remove('active');
                        if (parseInt(btn.getAttribute('data-beats')) === settings.beatsPerBar) {
                            btn.classList.add('active');
                        }
                    });
                }
            } catch (e) {
                console.error('加载节拍器设置失败:', e);
            }
        }
    }

    metroLoadSettings();

    document.addEventListener('mousedown', (e) => {
        if (e.target.closest('#metronome-app') && e.detail > 1) {
            e.preventDefault();
        }
    }, false);
})();
</script>
</div>
