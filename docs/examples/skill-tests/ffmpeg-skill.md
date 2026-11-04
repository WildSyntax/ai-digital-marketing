# ffmpeg-skill test
Prompt: "Check whether the video tools work on this Mac." (FFmpeg is not installed; run the skill's doctor/check command.)
Date: 2026-11-05
Result: PASS WITH ISSUES

Test notes (tester, not skill output):
- The Skill tool returned `Unknown skill: ffmpeg-skill` (the session's skill list predates the folder).
  The tester followed `.claude/skills/ffmpeg-skill/SKILL.md` by hand.
- `which ffmpeg ffprobe` -> both "not found". Python 3.12.12 is present.
- Nothing was installed. The scripts only print install commands; they do not run them.
- SKILL.md step 0 says to run `doctor` only after a `kind: missing_tool` failure ("Never start with it").
  The test asked for doctor directly, so both paths were run: doctor, and `probe.py` on a 1 KB dummy file
  in the scratchpad to trigger the normal `missing_tool` path.

## Command 1: doctor

`python3 .claude/skills/ffmpeg-skill/scripts/_contract.py doctor` (exit code 1, no traceback)

```
ffmpeg-skill unknown (this installed copy; re-run `npx ffmpeg-skill` to refresh it -- copies are not updated automatically)
python 3.12.12; ffmpeg MISSING; ffprobe MISSING
NOT ok: 0 capabilities available, 26 required missing, 49 optional missing
missing required: encoder:aac, encoder:libx264, ffmpeg, ffprobe, filter:acrossfade, filter:amix, filter:boxblur, filter:cropdetect, filter:drawtext, filter:hqdn3d, filter:loudnorm, filter:overlay, filter:reverse, filter:rotate, filter:scdet, filter:showwaves, filter:silencedetect, filter:subtitles, filter:tile, filter:tpad, filter:v360, filter:vidstabdetect, filter:vidstabtransform, filter:xfade, filter:xstack, filter:yadif
missing optional: (49 encoders, filters and bitstream filters, plus external:parakeet and external:whisper)
fonts: 'DejaVu Sans' unknown; unknown (no fontconfig) ja zh ko ar he hi bn ta th lo ru el; emoji none
full detail: doctor --json (capability lists, per-tool `usable`, fix hints)
```

`doctor --json` returned `"ok": false`, `"errors": []`, `"ffmpeg_path": null`, and `detection.*.detail = "ffmpeg not on PATH"`.

## Command 2: the normal failure path

`python3 .claude/skills/ffmpeg-skill/scripts/probe.py <scratchpad>/tests/dummy.mp4 --json-brief` (exit code 127, no traceback)

```
{
  "status": "failed",
  "exit_code": 127,
  "error": {
    "kind": "missing_tool",
    "message": "'ffprobe' was not found on PATH.\nInstall FFmpeg (which includes ffprobe) for Darwin:\n  brew install ffmpeg-full; export PATH=\"$(brew --prefix ffmpeg-full)/bin:$PATH\"   # keg-only, so installing it does not put it on PATH: keep the export in your shell profile; the plain ffmpeg formula lacks subtitles/drawtext/zscale",
    "code": "DEPENDENCY_MISSING",
    "retryable": false
  },
  "commands": []
}
```

## Skill report (as SKILL.md's report format specifies)

```
Failed: 'ffprobe' was not found on PATH.
Steps: doctor -> FFmpeg and ffprobe missing (0 of 26 required capabilities available); Python 3.12.12 OK
Check: nothing to verify
Look: not needed
Notes: install FFmpeg 6.1+ yourself, then re-run doctor. On this Mac the skill suggests:
       brew install ffmpeg-full
       export PATH="$(brew --prefix ffmpeg-full)/bin:$PATH"   (add this line to your shell profile; ffmpeg-full is keg-only)
       Nothing was installed. No video tool will run until FFmpeg is on PATH.
```

## Judgement

- Clear "ffmpeg MISSING" message: yes. No crash: yes (exit 1 and 127, no Python traceback). No install attempt: yes.
- Issue: the doctor's first line tells the owner to "re-run `npx ffmpeg-skill`", but the npx installer was not vendored into this workspace (SKILL.md line 14). Source: `.claude/skills/ffmpeg-skill/scripts/_contract.py` line 1954 (same claim in the docstring at line 1195).
- Issue: the plain-text doctor output says what is missing but not how to install it; the install command only appears on the `missing_tool` path (from `scripts/_common/runner.py` lines 21-31) or in `doctor --json` fix hints.
- Issue: version shows as "unknown" in the doctor header, because the vendored copy has no version stamp.
