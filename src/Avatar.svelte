<script>
  export let name
  export let email

  const DefaultColor = "#ffa500"

  $: initials = getInitials(name, email)
  $: color = getColor(name, email)



  const getInitials = (name, email) => {
    if (name) {
      return name.split(" ").map(x => x[0]).slice(0, 2).join("")
    } else if (email) {
      return email.slice(0, 2)
    } else {
      return "??"
    }
  }

  const hashCode = str => {
    let hash = 0
    if (!str?.length) {
      return hash
    }
    for (let i = 0; i < str.length; i++) {
      let chr = str.charCodeAt(i)
      hash = ((hash << 5) - hash) + chr
      hash |= 0 // Convert to 32bit integer
    }
    return hash
  }

  const getColor = (name, email) => {
    const seed = `${name || ""}${email || ""}`.toLowerCase()
    const hue = ((hashCode(seed) % 26) / 26) * 360
    return `hsl(${hue}, 50%, 50%)`
  }
</script>

<div class="avatar" style="--color: {color};">
  {initials}
</div>

<style>
  .avatar {
    flex: 0 0 40px;
    height: 40px;
    width: 40px;
    border-radius: 50%;
    display: grid;
    place-items: center;
    color: white;
    background: var(--color);
    font-weight: bold;
    font-size: 16px;
    text-transform: uppercase;
  }
</style>
