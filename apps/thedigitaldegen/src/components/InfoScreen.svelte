<script lang="ts">
    import { getGameService } from '../game/context';
    import { t } from '@lingui/macro';

    const gameService = getGameService();

    function closeInfo() {
        gameService.send('CLOSE_INFO');
    }
</script>

<div class="info-screen">
    <h2>{t`Game Info`}</h2>
    <p>This is where the game information and rules will go.</p>
    <!-- TODO: Add actual game rules and information -->
    <button on:click={closeInfo}>{t`Close`}</button>
</div>

<style>
    .info-screen {
        position: absolute;
        top: 50%;
        left: 50%;
        transform: translate(-50%, -50%);
        background-color: rgba(0, 0, 0, 0.8);
        color: white;
        padding: 20px;
        border-radius: 10px;
        z-index: 1000;
        text-align: center;
    }

    button {
        margin-top: 20px;
        padding: 10px 20px;
        background-color: #007bff;
        color: white;
        border: none;
        border-radius: 5px;
        cursor: pointer;
    }
</style>
