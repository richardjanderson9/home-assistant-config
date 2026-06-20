
# Smart Home Automation Configuration

This repository contains the version-controlled configuration and automation files for our smart home ecosystem. It utilises GitHub Actions for continuous integration (syntax validation) and automated deployment.

---

### Links (Private)
- [HA: Security Config](https://github.com/richardjanderson9/ha-security-config)
- [HA: Voice Patterns](https://github.com/richardjanderson9/ha-voice-patterns)

---

### Required Configurations Chnages

#### `/homeassistant/configuration.yaml`
```yaml
homeassistant:
  packages:
    custom: !include custom_configuration.yaml
```

#### `/homeassistant/custom_configuration.yaml`
```yaml
shell_command:
  git_sync: >-
    bash -c '
    if [ -d /config/github_sync/.git ]; then
      git -C /config/github_sync reset --hard &&
      git -C /config/github_sync pull --ff-only;
    else
      git clone [https://github.com/richardjanderson9/home-assistant-config.git](https://github.com/richardjanderson9/home-assistant-config.git) /config/github_sync;
    fi'
```