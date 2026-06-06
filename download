export default {
  async fetch(request, env, ctx) {
    const url = new URL(request.url);

    // Serve static assets from /public via Assets binding
    return env.ASSETS.fetch(request);
  },
};
